# Routine A: connectors-squad weekly synthesis

You are running the weekly synthesis routine for the **connectors-squad** Team OS repo as a
scheduled GitHub Actions job. This prompt is self-contained: all logic, formats, and
context you need are below. Do not look for external skills or heredocs — they are not
available in this environment.

---

## DRY_RUN behavior (read first)

The `DRY_RUN` environment variable controls whether this routine communicates with the
team. It defaults to `true`. Read it from the environment before doing anything else.

**Squad channel posting policy: this routine never posts to the public squad channel
(`#team-connectors`) under any DRY_RUN value.** That channel (and any engineering
channel) is scanned for data only — never written to. All notifications go to
`#distr-team-kb` and the PM DM, per the Slack notification format below.

- **`DRY_RUN=true` (default):** Do the full scan, analysis, and file generation. Create
  the branch and push it exactly as normal — a pushed branch with no PR yet is safe and
  does not broadcast to the team. Post to `#distr-team-kb` and send a Slack **DM to the
  PM** (Tony Smith, `UPQ9D0BFX`), both prefixed with `[DRY RUN]`.
- **`DRY_RUN=false`:** Communicate normally — post to `#distr-team-kb` and DM the PM per
  the steps below. No `[DRY RUN]` prefix. Still never post to `#team-connectors`.

If `DRY_RUN` is unset or any value other than the exact string `false`, treat it as `true`.

---

## Skills note

Claude Code skills (e.g. `domain-status-update`, `decision-logger`) live in the Cowork
environment and are **not accessible** in GitHub Actions runners. This prompt inlines all
the logic those skills would provide. Wherever the source spec says "invoke the
domain-status-update skill," follow the **Status.md format** section inlined below instead.
Do not attempt to call or load any skill.

---

## Global context (values already filled in for this squad)

```
SQUAD_NAME:        connectors-squad
PM_NAME:           Tony Smith
PM_SLACK_ID:       UPQ9D0BFX
REPO_OWNER:        toniaquino
REPO_NAME:         dev-tools-integrations-marketplace-kb
REPO_URL:          https://github.com/toniaquino/dev-tools-integrations-marketplace-kb
API_BASE:          https://api.github.com/repos/toniaquino/dev-tools-integrations-marketplace-kb
CLONE_URL:         https://toniaquino:$GH_PAT@github.com/toniaquino/dev-tools-integrations-marketplace-kb.git
CLONE_PATH:        /tmp/dev-tools-integrations-marketplace-kb
MAIN_BRANCH:       main
SQUAD_CHANNEL:     #team-connectors
SQUAD_CHANNEL_ID:  C06UC6RCV5G
HELP_CHANNEL:      #b-help-integrationshub
HELP_CHANNEL_ID:   C04B1TDAAS3
JIRA_BOARD_KEY:    INC
JIRA_SITE:         https://bynder.atlassian.net
# GH_PAT: provided as an environment variable by the workflow -- never hardcode or print it
# ATLASSIAN_API_TOKEN, ATLASSIAN_EMAIL: provided as environment variables -- see Jira API access below
```

**Ownership note:** Primary notification target for this routine is the PM (`PM_SLACK_ID`).
This routine does not open a PR or assign a reviewer -- Routine A2 does that once the
Slack thread confirms (see routine-a2.md), tagging `toniaquino` as reviewer at that point
(no squad GitHub usernames are configured yet).

**Timing note:** This synthesis runs Tuesdays but does not open a PR yet --
Routine A2 (Pass 2) opens the PR the following Wednesday evening (36 hours later), once
the Slack thread confirms (folding in any thread correction first) -- or once 36 hours
pass with no response at all, which counts as silent agreement. This repo IS the Team
Vault -- once the PR merges, the content is live here, no further weekly-sync step
elsewhere. The only case that doesn't open a PR that week is a reply that exists but
couldn't be parsed -- see Routine A2's failure handling.

---

## Repo access pattern

The workflow has already cloned the repo to `CLONE_PATH` before invoking you. Use that
clone. All writes follow this sequence:

```
# 1. Repo is already cloned at /tmp/dev-tools-integrations-marketplace-kb (CLONE_PATH).
#    If it is missing for any reason, clone it: git clone $CLONE_URL $CLONE_PATH
# 2. Read CLAUDE.md doc indexes to navigate -- do not explore blindly.
# 3. Write updated files.
# 4. Stage, branch, commit (full PR write-up as the commit message -- Routine A2 reads
#    this back to open the PR later), push:
git -C /tmp/dev-tools-integrations-marketplace-kb add -A
git -C /tmp/dev-tools-integrations-marketplace-kb checkout -b weekly-sync/connectors-synthesis-[YYYY-MM-DD]
git -C /tmp/dev-tools-integrations-marketplace-kb commit -F - <<'COMMIT_MSG'
Routine A: weekly synthesis [YYYY-MM-DD]

[Full PR description per the "PR description format" section below]
COMMIT_MSG
git -C /tmp/dev-tools-integrations-marketplace-kb push origin weekly-sync/connectors-synthesis-[YYYY-MM-DD]
# 5. Do NOT open a PR here. Routine A2 (Pass 2) opens the PR once the Slack thread gets
#    a 👍 or a parseable correction reply -- see routine-a2.md. This routine's job ends
#    once the branch is pushed.
# 6. Notify per the DRY_RUN rules above, linking the compare view since there is no PR
#    yet: https://github.com/toniaquino/dev-tools-integrations-marketplace-kb/compare/main...weekly-sync/connectors-synthesis-[YYYY-MM-DD]
# 7. Clean up only temp output files you created (not the repo clone the workflow manages).
```

Use today's UTC date for `[YYYY-MM-DD]`.

---

## Jira API access

**You have a Bash tool. Use it to run the exact `curl` command below. Do not use
WebFetch, do not use an MCP tool, do not search for a Jira integration — none of those
apply here. This is a plain authenticated HTTP call made via Bash, the same mechanism
you already use for the GitHub REST API calls in "Repo access pattern" above. If you
have not actually run this command in Bash and read its real output, you have not
checked Jira — do not write "Jira unavailable" until you have.**

Query Jira Cloud via the REST API using Basic auth built from `ATLASSIAN_EMAIL` and
`ATLASSIAN_API_TOKEN` (both provided as environment variables by the workflow -- never
hardcode or print them). Site: `https://bynder.atlassian.net`.

Run this now, via Bash:
```
curl -s -u "$ATLASSIAN_EMAIL:$ATLASSIAN_API_TOKEN" \
  -H "Accept: application/json" \
  -G "https://bynder.atlassian.net/rest/api/3/search/jql" \
  --data-urlencode "jql=project = INC AND updated >= -7d ORDER BY updated DESC" \
  --data-urlencode "fields=summary,status,updated,assignee,issuetype,parent" \
  --data-urlencode "maxResults=100"
```

This returns a JSON `issues` array. For each issue: `fields.status.name` is the current
status, `fields.updated` is the last-updated timestamp, `fields.issuetype.name`
distinguishes Epics from child issues, and `fields.parent.key` maps a child issue back to
its epic. Cross-reference epic keys against the ones already tracked in
`feature-index.yaml` to find status changes.

**Error handling for this call specifically -- based on the actual curl exit code and
HTTP status you observed, not an assumption:**
- HTTP 401 or 403: credentials are invalid or lack board access -- treat as "Jira
  unavailable" per Failure handling below, and say so explicitly (don't conflate this with
  a network outage).
- HTTP 200 with an empty `issues` array: a valid response -- nothing changed in the last 7
  days. This is not a failure.
- Any other non-200 response, or a curl network error (timeout, DNS failure, connection
  refused): treat as "Jira unavailable" per Failure handling below, and quote the actual
  curl output/error in the PR description as evidence.
- Never write "no live Jira API in this environment" or similar without having actually
  run the curl command above via Bash first.

---

## Slack API access

**You have a Bash tool. Use it to run the exact `curl` commands below. Do not use
WebFetch, do not use an MCP tool, do not search for a Slack integration — this is a
plain authenticated HTTP call via Bash, the same mechanism as the Jira and GitHub calls
elsewhere in this prompt. Slack's API returns HTTP 200 even when a call fails — always
check the `"ok"` field in the JSON body, not the HTTP status code. If you have not
actually run these commands in Bash and read their real JSON output, you have not
checked Slack — do not write "Slack unavailable" or "channel not accessible" until you
have.**

`conversations.history` requires a channel ID, not a channel name. **Use the hardcoded
IDs from Global context (`SQUAD_CHANNEL_ID`, `HELP_CHANNEL_ID`) directly -- do not
re-resolve channel names via `conversations.list` on every run.** These IDs were
confirmed live against the workspace on 2026-07-29 (`#team-connectors` = `C06UC6RCV5G`,
`#b-help-integrationshub` = `C04B1TDAAS3`). Confirmed with Tony Smith (PM) on 2026-07-30:
`#team-connectors` is the squad's main channel; `#b-help-integrationshub` is a secondary
channel worth scanning too. `#b-team-integrations` (previously listed in CLAUDE.md) is a
shared engineering channel spanning the Integrations, Connectors, and Tech Partners
squads, not primarily this squad's own -- not scanned here.

Fetch the last 7 days of messages for each channel, via Bash:
```
curl -s -H "Authorization: Bearer $SLACK_BOT_TOKEN" \
  -G "https://slack.com/api/conversations.history" \
  --data-urlencode "channel=<C06UC6RCV5G or C04B1TDAAS3 -- SQUAD_CHANNEL_ID or HELP_CHANNEL_ID>" \
  --data-urlencode "oldest=$(date -d '7 days ago' +%s)"
```

Check the JSON response -- based on what you actually observed, not an assumption:
- `"ok": true`: a real result. `"messages"` is the array to scan (an empty array just
  means no activity in the window -- not a failure).
- `"ok": false`: read the `"error"` field and quote it verbatim in the PR description.
  Common values: `not_in_channel` (the bot isn't a member of this channel -- a human
  needs to invite it), `missing_scope` (the bot token lacks a required OAuth scope),
  `invalid_auth` (the token itself is bad), `channel_not_found` (the hardcoded ID above
  is stale -- the channel was likely deleted or the workspace changed; do the fallback
  lookup below before reporting this as unavailable).
- A curl network error (timeout, DNS failure, connection refused) is a genuine
  connectivity failure -- distinct from an `"ok": false` API-level error. Report which
  one you actually got.

Never write "Slack unavailable" or "channel not accessible" without quoting which of the
above you actually got.

**Fallback -- only if `conversations.history` returns `channel_not_found` for the
hardcoded ID above.** Re-resolve the channel by paginating the full workspace list. This
call is NOT reliably a single page -- the workspace has 2000+ channels -- so you must
follow the cursor until it comes back empty, not just fetch once and stop:
```
cursor=""
while :; do
  resp=$(curl -s -H "Authorization: Bearer $SLACK_BOT_TOKEN" \
    -G "https://slack.com/api/conversations.list" \
    --data-urlencode "types=public_channel,private_channel" \
    --data-urlencode "limit=200" \
    --data-urlencode "cursor=$cursor")
  # scan resp's "channels" array for the target "name" (no leading "#") and record its "id" if found
  cursor=$(echo "$resp" | jq -r '.response_metadata.next_cursor // empty')
  [ -z "$cursor" ] && break
done
```
A single `limit=200` call with no cursor loop will silently miss channels once the
workspace exceeds one page -- this pattern caused false "channel not accessible" reports
in other squad KB repos (`tech-partners-squad-kb`, `organize-squad-kb`) even when the bot
was a member of the channel the whole time. If the fallback loop still doesn't find the
channel after exhausting `next_cursor`, then it's a genuine finding -- flag it and quote
the exhaustive page count actually observed.

---

## Purpose

Scan the prior 7 days of squad activity across Slack and Jira. Update `Status.md` files per
initiative and team area. Update `feature-index.yaml` for any status changes, and flag any shipped feature missing
artifacts (formerly Routine B, now Phase 2c below). Open one
draft PR. Notify per the DRY_RUN rules.

---

## Execution steps

### Phase 1: scan sources

Read `02 Teams/Connectors/CLAUDE.md` and its doc indexes only -- **not** the repo root
CLAUDE.md, which is the shared Dev Tools/Integrations/Marketplace overview covering
all three squads in this repo, not Connectors specifically. Do **not** read `Status.md` or PRD
files directly yet. For each initiative in the CLAUDE.md initiative list:

- **Slack:** scan the squad channel (`#team-connectors`, `SQUAD_CHANNEL_ID`) and the help
  channel (`#b-help-integrationshub`, `HELP_CHANNEL_ID`) for the last 7 days (see "Slack
  API access" above for how to query this -- use the hardcoded IDs directly). Extract
  status mentions, decision language, blocker language, and Jira ticket references. Use
  the PM-confirmed channels listed in `02 Teams/Connectors/CLAUDE.md`.
- **Jira:** query all active tickets on board `INC` (see "Jira API access" above for how
  to query this). Extract status changes in the last 7 days.
- **Apply source priority:** squad repo `Status.md` (current, as baseline) > Jira > Slack.

### Phase 2: update files

For each functional area, read its area `CLAUDE.md` and current `Status.md` files (all under `02 Teams/Connectors/product-development/`), then:

- Apply the **Status.md format** below (this replaces the `domain-status-update` skill).
- Apply the staleness check: if `Last reviewed` is past `Review due`, prepend a warning
  header to that Status.md noting it is overdue for human review.
- Write the updated `Status.md` content for that area.
- Do **not** modify PRDs, RFCs, or call summaries — those are human-authored.

(You may process areas sequentially; there is no need to spawn sub-agents in this runner.)

### Phase 2c: feature launch completeness check (formerly Routine B, now folded in)

Scan for Jira epics that moved to Done or Released in the last 7 days. Cross-reference
each against `feature-index.yaml`. Flag any shipped epic where the feature index status
is not updated or artifact paths are incomplete. This used to be a separate Friday
routine (Routine B) with no way to act on a reply; folding it in here means any missing
info a PM supplies in the Tuesday thread gets picked up by Routine A2 like any other
correction, instead of going nowhere.

**Step 1: pull shipped epics from Jira**

Query Jira with:

```
project = INC AND issuetype = Epic
AND status changed to (Done, Released) AFTER -7d
ORDER BY updated DESC
```

**Step 2: read feature-index.yaml**

The repo is already cloned at `/tmp/dev-tools-integrations-marketplace-kb` (read-only use). Read
`02 Teams/Connectors/product-development/product/feature-index.yaml`. For each shipped epic from Step 1, find
the matching feature-index entry by Jira epic key.

**Step 3: check completeness**

For each shipped epic:

| Check | Pass | Flag |
|---|---|---|
| Status field in feature-index.yaml | Shows ✅ Shipped | Shows any other emoji |
| PRD path | Points to an existing `.md` file | Empty, placeholder, or `tonysmith-ux` |
| Figma path | Points to a valid Figma URL | Empty or placeholder |
| Jira epic key | Matches the shipped epic | Missing |
| Customer context | `summary.md` exists for named customer accounts | No customer context for a customer-facing feature |

If any features are incomplete, list them under "Feature launch completeness" in the PR
description (see format below) and in the Slack notification, same thread as the weekly
synthesis ask -- do not send a separate DM or a separate #team-connectors post for
this. A reply supplying the missing info (PRD path, Figma link, customer context, etc.)
is a correction like any other -- Routine A2 folds it into `feature-index.yaml` before
opening the PR.

### Phase 3: compile and push branch (PR opens later, on confirmation)

- Write all updated `Status.md` files into the repo.
- Update `feature-index.yaml` status fields per the feature index update rule below.
- Follow the repo access pattern: branch, commit (full write-up as the commit message),
  push. Do **not** open a PR yet -- Routine A2 opens it once the Slack thread confirms
  (👍) or a correction is folded in.
- Notify per Phase 3a (scheduling) and the DRY_RUN rules below, linking the branch's
  compare view since there is no PR yet.
- Clean up any temp files you created.

### Phase 3a: schedule the Slack notification for Tony Smith's local 9am

**TEMPORARY (2026-07-20): hardcoded timezone.** Tony Smith's Slack timezone is
**America/New_York** (US Eastern). A live `users.info` lookup would be more robust but
needs the `users:read` Slack scope, which requires IT approval. Until that's granted,
use this hardcoded value (switch to `users.info` + `tz_offset` once the scope lands —
same scheduling logic below, just swap the timezone source).

1. Compose the message per the Slack notification format below.
2. Compute today's 9:00 AM in `America/New_York` as a UTC Unix timestamp
   (self-corrects for DST — no manual offset math):
   `target_utc=$(TZ="America/New_York" date -d "09:00" +%s)`.
3. If `target_utc` is already in the past (≤ now — e.g. Tony's 9am already passed
   before this run started), recompute for tomorrow instead:
   `target_utc=$(TZ="America/New_York" date -d "09:00 tomorrow" +%s)`.
4. If `target_utc` is more than ~5 minutes in the future, use
   `POST https://slack.com/api/chat.scheduleMessage` with `post_at=target_utc`. If it's
   sooner than that (already basically 9am there), `chat.postMessage` immediately.
5. `chat.scheduleMessage` returns a `scheduled_message_id`, not a real `ts`, until the
   message actually fires. Routine A2 (Pass 2) locates the notification via
   `conversations.history` by PR URL, so a missing real `ts` at this point is not an
   error.

---

## Status.md format (inlined — use this exact template)

```markdown
# [Initiative or team name]

**Owner:** [Full name]
**Status:** [emoji + one line -- see emoji rules below]
**Last updated:** [YYYY-MM-DD]
**Last reviewed:** [YYYY-MM-DD]
**Review due:** [YYYY-MM-DD -- 4 weeks from last reviewed unless specified]
**Source channels:** [#channel-name, #channel-name -- leave as TBD if unknown]

## Current state

- [Most recent development or milestone. Be specific -- "X shipped" not "things progressed"]
- [Second most recent or parallel workstream]
- [Any confirmed upcoming target or commitment]
- [Optional: context that helps the reader understand the above]

## Blockers

[Leave blank if none. Never write "None" -- just leave the section empty.]
- [Blocker name]: [what it gates]. Owner: [name]. Status: [one line].

## Commercial (Internal Only)

[Link to source only. Do not reproduce figures. Leave blank if no source link available.]
```

**Status emoji rules:**

| Emoji | When to use | Do not use when |
|---|---|---|
| ✅ | Work is fully shipped and in production | Anything is still in progress |
| 🟢 | On track, no blockers, hitting targets | There is any known risk, even minor |
| 🟡 | Known risk that may affect timeline or scope | The risk is actually blocking work |
| 🔴 | Cannot proceed without an external resolution | The blocker is internal and being worked |
| ⚪ | Not started, scope not confirmed, or deprioritized | Discovery has started |

When in doubt, use 🟡 and add a note. A false 🟢 is worse than an honest 🟡 — it misleads
the dependency alert routine and the GPM.

**Current state bullet rules:** Max 5 bullets; most recent first; one fact per bullet; past
tense for things that happened ("X shipped"), present tense for ongoing state ("Build in
progress"), future tense only for committed targets ("Launching Q3.1"). No speculation, no
personal assessments.

**Blockers section rules:** Only include blockers currently preventing work, or at risk of
blocking within 14 days. For each, name what it is, what it gates specifically, who owns
resolution (a person, not a team), and a one-line status.

---

## Feature index update rule

During weekly synthesis, update the `feature-index.yaml` status field for any feature whose
Jira epic status changed in the last 7 days -- the status emoji and the one-line summary.
Artifact paths (PRD, Figma, customer context) are handled separately by the feature launch
completeness check (Phase 2c) -- that phase flags gaps for shipped epics specifically; do not
duplicate that check here for non-shipped status changes.

---

## PR description format (used as the commit message body -- Routine A2 reuses it verbatim as the eventual PR body)

```
## Routine A: weekly synthesis -- [YYYY-MM-DD]

**Squad:** connectors-squad
**PM:** Tony Smith
**Files changed:** [list]

### What changed
[Bullet list of specific changes]

### Sources used
[Jira tickets (INC-XXXX), Slack channels referenced]

### Conflicts or gaps
[Source disagreements or missing data, or "None"]

### Feature launch completeness
[List any shipped epic found incomplete in Phase 2c: feature name, epic key, missing fields.
 Omit this section entirely if nothing shipped or everything was already complete.]

### Team Vault status
[This repo IS the Team Vault -- once merged, this content is live here directly, no
 further sync step. Note only if the change affects a cross-squad reference.]
```

---

## Slack notification format

Post to `#distr-team-kb` (<#C0BBHTHRSUC>) and DM the PM. Never post to `#team-connectors`
— it is scanned for data only, never written to, regardless of DRY_RUN.

There is no PR yet at this point -- link the branch's compare view instead:
`https://github.com/toniaquino/dev-tools-integrations-marketplace-kb/compare/main...weekly-sync/connectors-synthesis-[YYYY-MM-DD]`

When `DRY_RUN=false`:

```
<@UPQ9D0BFX> -- connectors-squad weekly synthesis proposed, not yet a PR.
What changed: [1-2 line summary]
Proposed changes: [compare URL]
Feature launch check: ["all shipped features complete", or list incomplete
  ones -- omit this line entirely if nothing shipped this week]

Reply "👍" or "confirmed" in this thread to open the PR as-is (this routine does not use Slack reactions for confirmation).
Reply in this thread with any corrections — Routine A2 folds them in and opens the PR
(Wednesday evening, 36h later, or sooner if triggered manually; silence at the
deadline is treated as agreement, not as no response).
Don't want to wait? Push directly to the branch above and open the PR yourself any time
— Slack is a convenience, not a requirement.
This repo IS the Team Vault -- once merged, this content is live here directly.
```

When `DRY_RUN=true`, use the same message prefixed with `[DRY RUN]` (also tag <@U0ACR39AJ79> (Bart) if content is relevant to his work) -- the PM tag is not optional in either branch:

```
[DRY RUN] <@UPQ9D0BFX> -- connectors-squad weekly synthesis (preview).
What changed: [1-2 line summary]
Proposed changes (draft): [compare URL]
```

---

## Failure handling

- **Jira unavailable:** proceed with a Slack-only scan. Note it in the PR description.
- **Slack channel not readable:** log it, skip that area, flag it in the PR description.
- **No changes detected:** do not push a branch (there is nothing for Routine A2 to open
  later). Post to `#distr-team-kb` (<#C0BBHTHRSUC>): `No squad changes detected this
  week.` (prefixed `[DRY RUN]` when `DRY_RUN=true`). Never post this to `#team-connectors`.
- **Push fails:** DM the PM (`UPQ9D0BFX`) with the generated Status.md content and the
  error details so nothing is lost.
