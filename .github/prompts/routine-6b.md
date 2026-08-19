# Routine 6B — Weekly status sync reply processing (Pass 2)

You are running headless in a GitHub Actions runner via `claude -p`. This prompt is
**self-contained**. Read it fully and execute it end to end. There is no human in the
loop during this run. This routine runs 36 hours after Pass 1 (routine-6.md). Pass 1
only pushes branches — it does not open PRs. This routine checks each area's thread
and, on a bare confirmation reply or a parseable correction, opens that area's PR
(folding in any correction first). No response by the 36-hour deadline is treated as
silent agreement — the PR opens as-is. Only a reply that exists but can't be parsed
blocks that area's PR — see Failure handling.

> **Provenance note (2026-08-19):** ported from
> `content-variations-delivery-performance-kb/.github/prompts/routine-6b.md`,
> simplified: no digest-manifest lookup, no Todd/Bart cc-thread handling (Todd Willms
> is a primary single-area owner here, confirming his own thread like Tony and Bas —
> there is no cross-cutting cc recipient in this domain). See `Governance.md` →
> "Routine 6" for why.

---

## Skills note — READ FIRST

Claude Code skills are **NOT available in this GitHub Actions runner**. Do not
invoke, load, or reference any skill. All logic is inlined below. **No MCP
connectors are configured** — talk to Slack through its REST API with `curl` and
`SLACK_BOT_TOKEN`. Do not call MCP tools.

---

## Diff safety note — READ FIRST

If you inspect what a branch actually changes for any reason, always diff against its
own merge-base with `main`, not against live current `main`:

    git merge-base main <branch>
    git diff <merge-base>..<branch>

Do **not** run `git diff main..<branch>` directly — `main` may have moved forward
independently since Pass 1 pushed the branch (unrelated PRs merging in the
meantime). That is normal branch staleness, not evidence of tampering.

---

## Environment & tooling

- `GH_PAT` — GitHub PAT for `toniaquino/dev-tools-integrations-marketplace-kb` (push + PR).
- `SLACK_BOT_TOKEN` — Slack bot token (`chat:write`, `channels:history`). Bearer auth.

(Routine 6B does not need Jira — it only reads Slack threads, edits `Status.md` files
on the branches Pass 1 pushed, and opens each PR once confirmed.)

Access patterns:

- **Git / repo:** pre-cloned at `/tmp/dev-tools-integrations-marketplace-kb`. Fetch +
  check out each pushed `status-sync/` branch. Push with
  `git -C /tmp/dev-tools-integrations-marketplace-kb push https://toniaquino:$GH_PAT@github.com/toniaquino/dev-tools-integrations-marketplace-kb.git <branch>`.
- **Slack read:** `conversations.replies` (Bearer `$SLACK_BOT_TOKEN`) for thread
  replies; `conversations.history` on `#distr-team-kb-log` (last ~3 days) to locate
  Pass 1's notification message if needed.
- **Slack write:** `chat.postMessage` for in-thread replies and `#distr-team-kb-log`
  posts. Tag recipients inline with `<@USER_ID>` — never DM (except Toni's summary,
  see Phase 3).
- **GitHub (find branches):** no PRs exist yet. Use
  `git ls-remote --heads https://toniaquino:$GH_PAT@github.com/toniaquino/dev-tools-integrations-marketplace-kb.git 'status-sync/*'`
  — one branch per area with changes.
- **GitHub (open a PR, once confirmed):**
  `POST https://api.github.com/repos/toniaquino/dev-tools-integrations-marketplace-kb/pulls`
  (Bearer `$GH_PAT`) with `draft:false`, `head:<branch>`, `base:main`, `title`, `body`;
  then `POST .../pulls/{number}/requested_reviewers` with that area's owner's GitHub
  username (from that squad's own `CLAUDE.md`; `toniaquino` if unset).

Confirm `"ok": true` (Slack) / HTTP 2xx (GitHub) before treating a call as successful.

---

## Global context

```
REPO:            github.com/toniaquino/dev-tools-integrations-marketplace-kb
SLACK_CHANNEL:   #distr-team-kb-log
TONI_SLACK_ID:   U9ATXKJM6
CLONE_PATH:      /tmp/dev-tools-integrations-marketplace-kb
MAIN_BRANCH:     main
```

---

## Gate

If no `status-sync/` branches exist on the remote, there is nothing to process — DM
Toni a one-line "no pending sync branches to process this week" and exit cleanly.

## Phase 1: locate each branch's thread

1. List remote branches matching `status-sync/*` via `git ls-remote --heads`. Each is
   one area's pushed branch (no PR yet).
2. For each branch, find its notification thread: read recent `#distr-team-kb-log`
   history (`conversations.history`, last ~3 days) for the Pass 1 message whose body
   contains that branch's compare URL
   (`https://github.com/toniaquino/dev-tools-integrations-marketplace-kb/compare/main...<branch>`),
   and use that message's `ts` as the thread root.

If no `status-sync/` branch and no matching thread can be found at all, DM Toni: "No
Routine 6 sync branches found for this week. Pass 1 may not have completed — check
its Actions run before relying on Pass 2." Then exit.

## Phase 2: process each thread

### Step 2a: check for a bare confirmation reply

Fetch replies (`conversations.replies` on the thread `ts`). Treat a reply as a bare
confirmation if its text, trimmed and lowercased, is exactly one of: `👍`, `+1`,
`confirmed`, `confirm`, `lgtm`, `approved`, `approve`. If present, treat the branch as
confirmed as-is — proceed to Phase 2b once Step 2b below has also run for this
thread. Note it in the Phase 3 summary as "confirmed via 👍". Still process any text
replies on the same thread per Step 2b — a bare confirmation and a reply are not
mutually exclusive.

### Step 2b: fetch and apply corrections

1. Fetch all replies in the thread.
2. Parse each for a concrete correction (status change, blocker update, decision
   note, channel correction).
3. Check out the branch in `/tmp/dev-tools-integrations-marketplace-kb`. Apply the
   correction to `Status.md`. Preserve existing content; adjust only what the reply
   specifies.
4. Commit `incorporate thread correction from [name] [YYYY-MM-DD]`, push to the same
   branch. Proceed to Phase 2b to open the PR with the correction folded in, then
   reply in thread with the resulting PR URL — do not reply here separately.

If a reply cannot be parsed into a concrete change, reply in thread: `I could not
parse your correction. Please edit the branch directly or describe the change more
specifically.` This does not, by itself, open the PR — a 👍 or a different, parseable
reply is still needed.

Threads with no replies at all: silent agreement — proceed to Phase 2b to open the PR
exactly as Pass 1 pushed it.

## Phase 2b: open the PR (per confirmed area)

For each area confirmed via 👍 in Step 2a, a parseable correction in Step 2b, or zero
replies (silence = agreement) — and only those. An area is excluded only when its
thread has a reply that exists but couldn't be parsed:

1. Retrieve Pass 1's original write-up from the branch's first commit:
   `git -C /tmp/dev-tools-integrations-marketplace-kb log <branch> --format=%B --reverse | head -n 50`.
   This is the PR body.
2. If a correction was folded in, append:
   `\n\n---\n_Correction from [name] applied from the Slack thread before this PR was opened._`
3. Open the PR via the GitHub REST API, targeting `main`:
   ```
   PR_RESPONSE=$(curl -s -X POST \
     -H "Authorization: Bearer $GH_PAT" \
     -H "Accept: application/vnd.github+json" \
     -H "Content-Type: application/json" \
     https://api.github.com/repos/toniaquino/dev-tools-integrations-marketplace-kb/pulls \
     -d '{"title":"Routine 6 weekly status sync: [area] [YYYY-MM-DD]","head":"<branch>","base":"main","body":"[body from steps 1-2 above]"}')
   ```
4. Extract the PR number and add the reviewer (that area's owner's GitHub username;
   `toniaquino` if unset):
   ```
   PR_NUMBER=$(echo "$PR_RESPONSE" | grep -o '"number":[0-9]*' | head -1 | grep -o '[0-9]*')
   curl -s -X POST \
     -H "Authorization: Bearer $GH_PAT" \
     -H "Accept: application/vnd.github+json" \
     https://api.github.com/repos/toniaquino/dev-tools-integrations-marketplace-kb/pulls/$PR_NUMBER/requested_reviewers \
     -d '{"reviewers":["<owner-github-username>"]}'
   ```
5. Reply in that thread:
   - Confirmed via 👍 only: `Opened the PR as confirmed: [PR URL]`
   - Correction folded in: `Got it — opened the PR with your correction folded in: [PR URL]`

## Phase 3: summarize to Toni

DM Toni (`U9ATXKJM6`) directly:

```
Weekly status sync Pass 2 complete — [YYYY-MM-DD]
Confirmed via 👍 (PR opened as-is): [N] ([list of areas])
Confirmed via silence (36h, no response, PR opened as-is): [N] ([list of areas])
PRs opened with corrections folded in: [N] ([list of areas])
Blocked on unparseable reply (branch still pending, no PR opened): [N] ([list of areas])
PRs opened this cycle: [list of PR URLs, or "none"]
```

---

## Success criteria

- Every pushed `status-sync/` branch's thread located via channel-history match on
  its compare URL.
- Every thread checked for a bare confirmation reply.
- Every reply either applied to its branch or flagged as unparseable.
- A PR opened per area confirmed via 👍, correction, or 36h silence — never when the
  thread has an unparseable reply.
- Correction commits pushed to the existing branch before PR creation.
- In-thread acknowledgements sent, including each PR URL.
- Pass 2 summary DMed to Toni.

## Failure handling

- No pushed sync branches: DM Toni (see Gate) and exit cleanly.
- Slack thread fetch fails for one branch: log it, continue with the others, note it
  in the Toni summary.
- A correction cannot be applied cleanly (merge conflict, file missing): leave the
  branch unchanged, reply in thread asking the owner to edit the branch directly, and
  note it in the Toni summary. Do not open a PR for that area.
- A thread has a reply that exists but could not be parsed: do not fabricate a PR.
  Note it in the Toni summary as pending; checked again next cycle or on manual
  trigger.
- PR-creation API call fails after confirmation: DM Toni with the branch name,
  confirmation status, and the error — the confirmed content is safe on the branch
  even though the PR didn't open.
- Push fails for a branch: log the error, DM Toni; do not abort other branches.
- Any uncaught fatal error: DM Toni with the routine name, the failed step, and the
  error text before exiting non-zero.
