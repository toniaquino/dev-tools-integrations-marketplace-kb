# Routine A2 — connectors-squad weekly synthesis reply processing (Pass 2)

You are running headless in a GitHub Actions runner via `claude -p`. This prompt is
**self-contained**. Read it fully and execute it end to end. There is no human in the
loop during this run. This routine runs Wednesday evening (36 hours after Tuesday's
Pass 1). Pass 1 only pushes a branch -- it does not open a PR. This routine checks the
Slack thread and, on a 👍 or a parseable correction reply, opens the PR (folding in any
correction first). No response by the 36-hour deadline is treated as silent
agreement -- the PR opens as-is, same as an explicit confirmation. Only a reply
that exists but can't be parsed blocks the PR -- see Failure handling.

---

## Skills note — READ FIRST

Claude Code skills are **NOT available in this GitHub Actions runner**. Do not invoke,
load, or reference any skill. All logic is inlined below.

**No MCP connectors are configured** in this runner. Talk to Slack through its REST API
with `curl` and `SLACK_BOT_TOKEN`. Do not call MCP tools.

---

## Diff safety note — READ FIRST

If you inspect what a branch actually changes for any reason (sanity-checking scope,
confirming what a correction reply is being applied on top of, or just understanding
what Pass 1 did), always diff the branch against its own merge-base with `main`, not
against live current `main`:

    git merge-base main <branch>
    git diff <merge-base>..<branch>

Do **not** run `git diff main..<branch>` directly. This routine runs days after Pass 1
pushed the branch, so `main` may have moved forward independently in the meantime --
other PRs merging unrelated fixes to the same files, for instance. A raw diff against a
moved `main` will show those unrelated changes as if the branch made them. That is
normal branch staleness, not evidence of tampering, and is not grounds for withholding
a PR or escalating a security concern. If the branch's own commits (`git log
main..<branch> --oneline`, scoped correctly via merge-base) touch only the files their
commit messages say they touch, the branch is fine.

---

## Environment & tooling

Available environment variables:

- `GH_PAT` — fine-grained GitHub PAT for `toniaquino/dev-tools-integrations-marketplace-kb` (push + PR).
- `SLACK_BOT_TOKEN` — Slack bot token (`chat:write`, `channels:history`). Bearer auth.

(Routine A2 does not need Jira/Confluence — it only reads Slack threads, edits files on
the branch Pass 1 pushed, and opens the PR once confirmed.)

Access patterns:

- **Git / repo:** clone fresh at `/tmp/dev-tools-integrations-marketplace-kb` if not already present:
  `git clone https://toniaquino:$GH_PAT@github.com/toniaquino/dev-tools-integrations-marketplace-kb.git /tmp/dev-tools-integrations-marketplace-kb`.
  Fetch + check out the pushed `weekly-sync/connectors-synthesis-` branch (no PR exists yet). Push
  with
  `git -C /tmp/dev-tools-integrations-marketplace-kb push https://toniaquino:$GH_PAT@github.com/toniaquino/dev-tools-integrations-marketplace-kb.git <branch>`.
- **Slack read:** `conversations.replies` (Bearer `$SLACK_BOT_TOKEN`) to fetch thread
  replies; `conversations.history` on `#distr-team-kb-log` (channel ID `C0BL0BZQFNX` --
  use this directly, do not resolve the name via `conversations.list`) to locate the
  Tuesday notification message.
- **Slack write:** `chat.postMessage` for in-thread replies. Tag recipients inline with
  `<@USER_ID>` — never DM for thread replies.
- **GitHub (find the branch):** there is no PR to list yet. Use
  `git ls-remote --heads https://toniaquino:$GH_PAT@github.com/toniaquino/dev-tools-integrations-marketplace-kb.git 'weekly-sync/connectors-synthesis-*'`
  to find the pushed branch.
- **GitHub (open the PR, once confirmed):**
  `POST https://api.github.com/repos/toniaquino/dev-tools-integrations-marketplace-kb/pulls` (Bearer
  `$GH_PAT`) with `draft:true`, `head:<branch>`, `base:main`, `title`, `body`. Do not
  attempt a `requested_reviewers` call afterward -- `GH_PAT` authenticates as
  `toniaquino`, the same identity that authors the PR, and GitHub rejects a
  self-review request outright (this is a platform rule, not a permissions gap that
  can be fixed by reconfiguring the token). The Phase 3 DM to the PM, which includes
  the PR URL, is the actual "please look at this" signal -- it doesn't depend on
  collaborator status the way a reviewer request would.

Confirm `"ok": true` (Slack) / HTTP 2xx (GitHub) before treating a call as successful.

---

## Global context (shared constants — inlined)

```
SQUAD_NAME:      connectors-squad
PM_NAME:         Tony Smith
PM_SLACK_ID:     UPQ9D0BFX
REPO_OWNER:      toniaquino
REPO_NAME:       dev-tools-integrations-marketplace-kb
CLONE_PATH:      /tmp/dev-tools-integrations-marketplace-kb
MAIN_BRANCH:     main
SLACK_CHANNEL:   #distr-team-kb-log
```

---

## Gate

Routine A2 should only be active once Routine A is running. If no remote branch
matching `weekly-sync/connectors-synthesis-*` exists, DM `UPQ9D0BFX` a one-line "no pending sync
branch to process this week" and exit cleanly.

---

## Phase 1: locate Pass 1 state

### Step 1: find the pushed branch and its notification thread

1. List remote branches matching `weekly-sync/connectors-synthesis-*` via `git ls-remote --heads`.
   There should be at most one (this squad's Routine A pushes a single branch per run,
   not per-owner). If more than one exists, use the most recently pushed (by commit
   date).
2. Read recent `#distr-team-kb-log` history (`conversations.history`, last ~4 days) to find
   the Tuesday notification message whose body contains that branch's compare URL
   (`https://github.com/toniaquino/dev-tools-integrations-marketplace-kb/compare/main...<branch>`). Use
   that message's `ts` as the thread root.

If no `weekly-sync/connectors-synthesis-` branch can be found, DM `UPQ9D0BFX`:
"No Routine A sync branch found for this week. Pass 1 may not have completed — check the
Routine A Actions run before relying on Pass 2." Then exit.

If the branch is found but the notification message cannot be located in
`#distr-team-kb-log` history, proceed to Phase 2 anyway using an empty reply set, and note
this in the Phase 3 summary rather than failing the run.

## Phase 2: process thread replies

### Step 2a: check for a bare confirmation reply (opens the PR as-is)

This routine does not use Slack reactions for confirmation -- the bot token lacks
the `reactions:read` scope, and that scope is not always grantable. Fetch the
thread's replies (`conversations.replies` on the thread `ts` -- the same call used
in Step 2 below, no need to call it twice). If any reply from `UPQ9D0BFX`, trimmed and
lowercased, is exactly one of: `👍`, `+1`, `confirmed`, `confirm`, `lgtm`,
`approved`, `approve` -- treat this as confirmed, no file changes needed, proceed to
Phase 2b to open the PR exactly as Pass 1 pushed it. Note it in the Phase 3 summary
as "confirmed via 👍". Still process any other, substantive replies on the same
thread per Step 2 below -- a bare confirmation and a separate correction reply are
not mutually exclusive.

### Step 2: fetch and apply corrections

If the thread has replies (`conversations.replies` on the thread `ts`):

1. Fetch all replies in the thread.
2. Parse each reply for corrections or added context (status changes, blocker updates,
   feature-index corrections, channel corrections).
3. Check out the `weekly-sync/connectors-synthesis-` branch in `/tmp/dev-tools-integrations-marketplace-kb` (clone
   the repo fresh if that path isn't already present).
4. Apply the correction to the relevant `Status.md` or `feature-index.yaml` file
   (both under `02 Teams/Connectors/product-development/`).
   Preserve existing content; prepend/adjust per the reply. Do not delete unless the
   reply explicitly contradicts existing content.
5. Commit and push to the same branch:
   `incorporate thread correction from Tony Smith [YYYY-MM-DD]`.
6. Proceed to Phase 2b to open the PR with the correction folded in, then reply in
   thread with the resulting PR URL (see Phase 2b) — do not reply here separately.

If a reply cannot be parsed into a concrete change, reply in thread:
`I could not parse your correction. Please edit the branch directly or describe the
change more specifically.` This does not, by itself, open the PR — a 👍 or a different,
parseable reply is still needed.

No replies at all: this is silent agreement, not a block. Proceed to Phase 2b to
open the PR exactly as Pass 1 pushed it. Note it in the Phase 3 summary as
"confirmed via silence (36h, no response)". This is different from a reply that
exists but couldn't be parsed -- see Failure handling for that case, which does
block the PR.

## Phase 2b: open the PR

Reach this phase if Step 2a found a bare confirmation, Step 2 applied at least one
parseable correction, or the thread has zero replies at all (silence = agreement,
36h deadline). The only case that does NOT reach this phase: a reply exists but
couldn't be parsed into a concrete change -- that's an active response needing
human clarification, not silence, and must not be treated as agreement.

1. Retrieve Pass 1's original write-up from the branch's first commit:
   `git -C /tmp/dev-tools-integrations-marketplace-kb log <branch> --format=%B --reverse | head -n 50`
   (the first commit Pass 1 made contains the full PR description as its commit
   message). This is the PR body.
2. If a correction was folded in during Step 2, append to the body:
   `\n\n---\n_Correction from Tony Smith applied from the Slack thread before this PR was opened._`
3. Open the PR via the GitHub REST API (draft, targeting `main`):
   ```
   PR_RESPONSE=$(curl -s -X POST \
     -H "Authorization: Bearer $GH_PAT" \
     -H "Accept: application/vnd.github+json" \
     -H "Content-Type: application/json" \
     https://api.github.com/repos/toniaquino/dev-tools-integrations-marketplace-kb/pulls \
     -d '{"title":"Routine A: weekly synthesis [YYYY-MM-DD]","head":"<branch>","base":"main","body":"[body from steps 1-2 above]","draft":true}')
   ```
   Do not follow up with a `requested_reviewers` call -- see the reviewer note under
   Access patterns above. The Phase 3 DM is the notification.
4. Reply in the Slack thread:
   - Confirmed via 👍 only: `Opened the PR as confirmed: [PR URL]`
   - No response within 36h: `No response in 36h, opening the PR as proposed: [PR URL]`
   - Correction folded in: `Got it — opened the PR with your correction folded in: [PR URL]`

## Phase 3: summarize to PM

DM `UPQ9D0BFX` directly:

```
connectors-squad weekly synthesis Pass 2 complete — [YYYY-MM-DD]
Confirmed via 👍: [yes/no]
Confirmed via silence (36h, no response): [yes/no]
Correction folded in: [yes/no]
Replies that could not be parsed: [count, or "none"]
PR opened: [PR URL, or "not opened — unparseable reply needs clarification, branch still pending"]
```

---

## Success criteria

- Pass 1 state located (pushed branch + its notification thread, where findable).
- Thread checked for a 👍 confirmation and logged as confirmed if present.
- Any thread reply either applied to the branch or flagged as unparseable.
- PR opened via the GitHub API for: confirmed via 👍, a correction applied, or the
  36-hour window elapsing with zero replies (silence = agreement). Never opened
  when a reply exists but couldn't be parsed -- that needs human clarification.
- Correction commits pushed to the branch before PR creation (not a separate branch).
- In-thread acknowledgements sent, including the new PR URL once opened.
- Pass 2 summary DMed to `UPQ9D0BFX`.

## Failure handling

- No `weekly-sync/connectors-synthesis-` branch found: DM `UPQ9D0BFX` (see Gate) and exit
  cleanly.
- Notification message not found in `#distr-team-kb-log` history: proceed with no replies
  to process, note it in the Phase 3 summary.
- Slack thread fetch fails: log it, note it in the Phase 3 summary, do not fail the run.
- A correction cannot be applied cleanly (merge conflict, file missing): leave the
  branch unchanged, reply in thread asking to edit the branch directly, note it in the
  summary. Do not open a PR in this case.
- A reply exists but could not be parsed into a concrete change: do not
  fabricate a PR (this is the one case silence-as-agreement does not cover --
  someone responded, the routine just couldn't understand it). Reply in thread
  asking for clarification (see Step 2), and DM `UPQ9D0BFX` noting the branch
  is still pending and will be checked again next cycle (or on manual trigger).
- PR-creation API call fails after confirmation: DM `UPQ9D0BFX` with the branch name,
  confirmation status, and the error — the confirmed content is safe on the branch even
  though the PR didn't open.
- Push fails: log the error, DM `UPQ9D0BFX` with the branch name and error.
- Any uncaught fatal error: DM `UPQ9D0BFX` with the routine name, the failed step, and
  the error text before exiting non-zero.
