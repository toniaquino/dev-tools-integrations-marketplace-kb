# Routine A: weekly synthesis — Technology Partners squad

**DRY_RUN behaviour:** Check the DRY_RUN environment variable before any write operation.
This routine always does the full scan, writes Status.md, and pushes the branch --
a pushed branch with no PR yet is safe and does not broadcast to the team. DRY_RUN only
controls the `[DRY RUN]` prefix on notifications; it never skips branch/commit/push.
- `DRY_RUN=true`: full run; the `#distr-team-kb-log` post and the TONI_SLACK_ID DM are both
  prefixed with `[DRY RUN]`.
- `DRY_RUN=false` (default): full run; no prefix.
Always log DRY_RUN value at the start: "Routine A starting. DRY_RUN=[value]."

**Skills note:** Claude Code skills (domain-status-update, blocker-escalation, etc.) are not
available in this GitHub Actions environment. All skill logic is inlined in this prompt.

---

## Global context

```
SQUAD_NAME:            tech-partners-squad
PM_NAME:               Bas van Reeuwijk
PM_SLACK_ID:           U04H9D3H14K
TONI_SLACK_ID:         U9ATXKJM6
REPO_OWNER:            toniaquino
REPO_NAME:             dev-tools-integrations-marketplace-kb
CLONE_PATH:            /tmp/dev-tools-integrations-marketplace-kb
CLONE_URL:             https://toniaquino:$GH_PAT@github.com/toniaquino/dev-tools-integrations-marketplace-kb.git
API_BASE:              https://api.github.com/repos/toniaquino/dev-tools-integrations-marketplace-kb
SQUAD_CHANNEL:         #b-team-integrations
SQUAD_CHANNEL_ID:      C5XR6FERK
SECONDARY_CHANNEL:     #b-help-global-partnerships
SECONDARY_CHANNEL_ID:  C02KQ068K1T
CONFLUENCE_SPACE:      INTEGRATE
CONFLUENCE_URL:        https://bynder.atlassian.net/wiki/spaces/INTEGRATE/overview
JIRA_BOARD_KEY:        MP
MAIN_BRANCH:        main
```

Jira board: MP (confirmed with Bas van Reeuwijk, 2026-07-08).

**Ownership note:** This routine does not open a PR or assign a reviewer -- Routine A2
does that once the Slack thread confirms (see routine-techpartners-a2.md). Routine A2
does not attempt a reviewer-request call at all: `GH_PAT` authenticates as `toniaquino`,
the same identity that opens the PR, and GitHub rejects self-review requests outright.
The Phase 3 DM to Bas already carries the PR URL and is the actual notification.

**Team Vault note:** This synthesis runs Tuesdays but does not open a PR yet -- Routine
A2 (Pass 2) opens the PR the following Wednesday evening (36 hours later), once the
Slack thread confirms (folding in any thread correction first) -- or once 36 hours pass
with no response at all, which counts as silent agreement. This repo IS the Team Vault
-- once merged, this content is live here directly, no further sync step. The only case
that doesn't open a PR that week is a reply that exists but couldn't be parsed -- see
Routine A2's failure handling.

---

## Jira API access

**You have a Bash tool. Use it to run the exact `curl` command below. Do not use
WebFetch, do not use an MCP tool, do not search for a Jira integration — none of those
apply here. This is a plain authenticated HTTP call made via Bash, the same mechanism
you already use for the GitHub REST API calls elsewhere in this prompt. If you have not
actually run this command in Bash and read its real output, you have not checked Jira —
do not write "Jira unavailable" until you have.**

Query Jira Cloud via the REST API using Basic auth built from `ATLASSIAN_EMAIL` and
`ATLASSIAN_API_TOKEN` (both provided as environment variables by the workflow -- never
hardcode or print them). Site: `https://bynder.atlassian.net`.

Run this now, via Bash:
```
curl -s -u "$ATLASSIAN_EMAIL:$ATLASSIAN_API_TOKEN" \
  -H "Accept: application/json" \
  -G "https://bynder.atlassian.net/rest/api/3/search/jql" \
  --data-urlencode "jql=project = MP AND updated >= -7d ORDER BY updated DESC" \
  --data-urlencode "fields=summary,status,updated,assignee,issuetype,parent" \
  --data-urlencode "maxResults=100"
```

This returns a JSON `issues` array. For each issue: `fields.status.name` is the current
status, `fields.updated` is the last-updated timestamp, `fields.issuetype.name`
distinguishes Epics from child issues, and `fields.parent.key` maps a child issue back to
its epic. Cross-reference epic keys against the four tracked features in
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
plain authenticated HTTP call via Bash, the same mechanism as the GitHub REST API calls
elsewhere in this prompt. Slack's API returns HTTP 200 even when a call fails — always
check the `"ok"` field in the JSON body, not the HTTP status code. If you have not
actually run these commands in Bash and read their real JSON output, you have not
checked Slack — do not write "Slack unavailable" or "channel not accessible" until you
have.**

`conversations.history` requires a channel ID, not a channel name. **Use the hardcoded
IDs from Global context (`SQUAD_CHANNEL_ID`, `SECONDARY_CHANNEL_ID`) directly -- do not
re-resolve channel names via `conversations.list` on every run.** Those IDs were
confirmed live against the workspace on 2026-07-29 (`#b-team-integrations` =
`C5XR6FERK`, `#b-help-global-partnerships` = `C02KQ068K1T`).

Fetch the last 7 days of messages for each channel, via Bash:
```
curl -s -H "Authorization: Bearer $SLACK_BOT_TOKEN" \
  -G "https://slack.com/api/conversations.history" \
  --data-urlencode "channel=<C5XR6FERK or C02KQ068K1T -- SQUAD_CHANNEL_ID or SECONDARY_CHANNEL_ID>" \
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

**Fallback -- only if `conversations.history` returns `channel_not_found` for a hardcoded
ID above.** Re-resolve the channel by paginating the full workspace list. This call is
NOT reliably a single page -- the workspace has 200+ channels -- so you must follow the
cursor until it comes back empty, not just fetch once and stop:
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
workspace exceeds one page -- this is what caused two consecutive cycles (2026-07-20,
2026-07-28) to falsely report `#b-help-global-partnerships` as not found even though the
bot was a member of it the whole time. If the fallback loop still doesn't find the
channel after exhausting `next_cursor`, then it's a genuine finding -- flag it and quote
the exhaustive page count actually observed.

---

## Phase 1 — scan Slack

Scan the following channels for the last 7 days (see "Slack API access" above for how
to query this):

**#b-team-integrations** (primary squad channel)
Extract: delivery status signals, partner mentions, decisions, blockers.

**#b-help-global-partnerships** (partner workflow context)
Extract: partner escalations, integration blockers, certification updates.

For each channel, extract signals for the four tracked features:
- Integration Abstraction Layer (IAL)
- Certification Program
- Doc Migration
- Partner Onboarding

Signal priority:
- Explicit status statements from Bas > inferred signals from thread replies
- Named blockers > general discussion
- Most recent signal wins if conflicting

---

## Phase 2 — scan Jira

Query Jira board `MP` for issues updated in the last 7 days (see "Jira API access"
above for how to query this). Cross-reference epic keys against the four tracked
features:
- Integration Abstraction Layer (IAL)
- Certification Program
- Doc Migration
- Partner Onboarding

Extract status changes, blockers noted in Jira fields, and any epic that moved to
Done/Released.

---

## Phase 3 — scan Confluence

Check the INTEGRATE space for pages updated since last Monday.
Focus areas:
- Integration Abstraction Layer pages (blueprint, RFC, status updates)
- Bynder Integration Certification Program pages (partner enrollment, status)
- Partner Integrations and Connectors overview pages

Extract:
- Status changes to any of the four tracked features
- New decisions or scope changes documented in Confluence
- Partner additions, removals, or escalations

---

## Phase 4 — read current squad repo state

The repo is already cloned at CLONE_PATH. Read:
- `02 Teams/Technology Partners/CLAUDE.md` and its doc indexes only -- **not** the repo
  root `CLAUDE.md`, which is the shared Dev Tools/Integrations/Marketplace overview
  covering all three squads in this repo, not Technology Partners specifically.
- `02 Teams/Technology Partners/product-development/product/feature-index.yaml` — current feature statuses
- `02 Teams/Technology Partners/product-development/product/PRDs/integrations-marketplace/CLAUDE.md` — current initiative status
- `02 Teams/Technology Partners/product-development/product/PRDs/integrations-marketplace/Status.md` — current status if present

Navigate using CLAUDE.md doc indexes only. Do not read all files.

---

## Phase 5 — apply source priority

| Content type | Source priority |
|---|---|
| Delivery status | Jira (status field, authoritative) > Slack (most recent explicit signal) > Confluence > current feature-index.yaml value |
| Decisions | Slack (decisions surface here first) > Confluence |
| Blockers | Jira (explicit blocked status) > Slack > Confluence |
| Partner context | Confluence > Slack |

If sources conflict and cannot be auto-resolved: flag in PR description. Do not guess.

---

## Phase 6 — write Status.md

Write to `02 Teams/Technology Partners/product-development/product/PRDs/integrations-marketplace/Status.md`.
Create the file if it does not exist. Use this exact format:

```markdown
# Integrations Marketplace -- status

**Last updated:** YYYY-MM-DD
**PM:** Bas van Reeuwijk
**Status:** [emoji]

## This week

[2-4 bullets: what moved, what shipped, what was decided. Source each signal.]

## Blockers

[Named blockers with owner. "None" if clear.]

## Coming up

[1-3 items expected next week based on Jira, Slack, and Confluence signals.]

## Features

| Feature | Status | Last signal |
|---|---|---|
| Integration Abstraction Layer | [status] | [date + source] |
| Certification Program | [status] | [date + source] |
| Doc Migration | [status] | [date + source] |
| Partner Onboarding | [status] | [date + source] |
```

Status emoji legend:
🟢 On track | 🟡 In progress / some risk | 🔴 Blocked | ⚫ Deprioritised | ✅ Shipped | ⚪ No update

---

## Phase 7 — update feature-index.yaml if signals warrant

If Jira, Slack, or Confluence signals a status change for a tracked feature, update the
`status` field in `02 Teams/Technology Partners/product-development/product/feature-index.yaml` and add a
`last_signal` note with date and source.

Do not update if the only signal is absence of news.

---

## Phase 7b — feature launch completeness check (formerly Routine B, now folded in)

Scan for Jira epics that moved to Done or Released in the last 7 days. Cross-reference
each against `feature-index.yaml`. Flag any shipped epic where the feature index status
is not updated or artifact paths are incomplete. This used to be a separate Friday
routine (Routine B) with no way to act on a reply; folding it in here means any missing
info Bas supplies in the Tuesday thread gets picked up by Routine A2 like any other
correction, instead of going nowhere.

**Step 1: pull shipped epics from Jira**

Query Jira with:

```
project = MP AND issuetype = Epic
AND status changed to (Done, Released) AFTER -7d
ORDER BY updated DESC
```

**Step 2: read feature-index.yaml**

Read `02 Teams/Technology Partners/product-development/product/feature-index.yaml`. For each shipped epic from Step
1, find the matching feature-index entry by Jira epic key.

**Step 3: check completeness**

For each shipped epic:

| Check | Pass | Flag |
|---|---|---|
| Status field in feature-index.yaml | Shows ✅ Shipped | Shows any other emoji |
| PRD path | Points to an existing `.md` file | Empty or placeholder |
| Figma path | Points to a valid Figma URL | Empty or placeholder |
| Jira epic key | Matches the shipped epic | Missing |
| Customer context | `summary.md` exists for named customer accounts | No customer context for a customer-facing feature |

If any features are incomplete, list them under "Feature launch completeness" in the PR
description (Phase 8) and in the Slack notification (Phase 9), same thread as the
weekly synthesis ask -- do not send a separate DM or a separate `#distr-team-kb-log` post
for this. A reply supplying the missing info (PRD path, Figma link, customer context,
etc.) is a correction like any other -- Routine A2 folds it into `feature-index.yaml`
before opening the PR.

---

## Phase 8 — commit, push branch (PR opens later, on confirmation)

Always run this phase, regardless of DRY_RUN -- a pushed branch with no PR yet is safe.
See DRY_RUN behaviour above.

Branch: `weekly-sync/techpartners-synthesis-[DATE]`
Commit: use `git commit -F - <<'COMMIT_MSG' ... COMMIT_MSG` with the **full PR
write-up below (verbatim, not a one-line summary) as the commit message** -- Routine A2
reads this commit message back to build the PR body once the Slack thread confirms.
Push the branch. Do **not** open a PR here and do **not** add a reviewer -- Routine A2
opens the PR once the thread gets a 👍 or a parseable correction reply. This routine's
job ends once the branch is pushed. Notify per Phase 9 below, linking the branch's
compare view since there is no PR yet, using the scheduling logic in Phase 9a.

PR description (used as the commit message body -- Routine A2 reuses it verbatim as the
eventual PR body):
```
## Routine A: weekly synthesis -- [DATE]

**Squad:** Technology Partners
**Sources:** Jira (board MP), Slack (#b-team-integrations, #b-help-global-partnerships), Confluence (INTEGRATE space)
**DRY_RUN:** false
**Files changed:** [list]

### What changed
[Bullets]

### Sources used
- Jira: board MP ([N] issues updated)
- Slack: #b-team-integrations ([N] signals), #b-help-global-partnerships ([N] signals)
- Confluence: [page names referenced]

### Conflicts flagged
[Source disagreements or "None"]

### Staleness flags
[Files past review cadence or "None"]

### Feature launch completeness
[List any shipped epic found incomplete in Phase 7b: feature name, epic key, missing
 fields. Omit this section entirely if nothing shipped or everything was already
 complete.]

### Team Vault status
This repo IS the Team Vault -- once merged, this content is live here directly, no
further sync step.
```

---

## Phase 9 — Slack notification

Post to `#distr-team-kb-log` (<#C0BL0BZQFNX>) and DM TONI_SLACK_ID. Never post to
`#b-team-integrations` or `#b-help-global-partnerships` under any DRY_RUN value — those
channels are scanned for data only (Phase 1), never written to.

There is no PR yet at this point -- link the branch's compare view instead:
`https://github.com/toniaquino/dev-tools-integrations-marketplace-kb/compare/main...weekly-sync/techpartners-synthesis-[DATE]`

Format for the `#distr-team-kb-log` post (prefix with `[DRY RUN]` when DRY_RUN=true). Use
the literal Slack mention syntax `<@U04H9D3H14K>` below -- not the bare ID as plain
text, which renders as unlinked, non-notifying text:
```
<@U04H9D3H14K> -- Technology Partners weekly synthesis proposed, not yet a PR.
What changed: [1-2 line summary]
Conflicts: [flagged or "none"]
Feature launch check: ["all shipped features complete", or list incomplete ones --
  omit this line entirely if nothing shipped this week]
Proposed changes: [compare URL]

Reply "👍" or "confirmed" in this thread to open the PR as-is (this routine does not use Slack reactions for confirmation).
Reply in this thread with any corrections — Routine A2 folds them in and opens the PR
(Wednesday evening, 36h later, or sooner if triggered manually; silence at the
deadline is treated as agreement, not as no response).
Don't want to wait? Push directly to the branch above and open the PR yourself any time
— Slack is a convenience, not a requirement.
```

If DRY_RUN=true: also DM TONI_SLACK_ID with:
"[DRY RUN] Routine A complete -- [DATE]
What changed: [summary]
Status.md preview: [first 10 lines of generated content]
Proposed changes (draft): [compare URL]"

### Phase 9a — schedule the `#distr-team-kb-log` post for Bas van Reeuwijk's local 9am

**TEMPORARY (2026-07-20): hardcoded timezone.** Bas van Reeuwijk's Slack timezone is
**Europe/Amsterdam** (Amsterdam, CET). A live `users.info` lookup would be more robust
but needs the `users:read` Slack scope, which requires IT approval. Until that's
granted, use this hardcoded value (switch to `users.info` + `tz_offset` once the scope
lands — same scheduling logic below, just swap the timezone source).

1. Compose the `#distr-team-kb-log` message per Phase 9 above.
2. Compute today's 9:00 AM in `Europe/Amsterdam` as a UTC Unix timestamp
   (self-corrects for DST — no manual offset math):
   `target_utc=$(TZ="Europe/Amsterdam" date -d "09:00" +%s)`.
3. If `target_utc` is already in the past (≤ now — e.g. Bas's 9am already passed
   before this run started), recompute for tomorrow instead:
   `target_utc=$(TZ="Europe/Amsterdam" date -d "09:00 tomorrow" +%s)`.
4. If `target_utc` is more than ~5 minutes in the future, use
   `POST https://slack.com/api/chat.scheduleMessage` with `post_at=target_utc`. If it's
   sooner than that (already basically 9am there), `chat.postMessage` immediately. This
   scheduling applies only to the `#distr-team-kb-log` post — the TONI_SLACK_ID DM (DRY_RUN
   preview only) still sends immediately.
5. `chat.scheduleMessage` returns a `scheduled_message_id`, not a real `ts`, until the
   message actually fires. Routine A2 (Pass 2) locates the notification via
   `conversations.history` by the branch's compare URL, so a missing real `ts` at this
   point is not an error.

---

## Failure handling

- Jira unavailable: proceed without the Jira scan, note it in the PR description, quote
  the actual curl output/error as evidence
- Slack channel unreadable: skip that channel, flag in PR description, DM TONI_SLACK_ID
- Confluence unavailable: proceed without it, note in PR description
- No changes detected: do not push a branch (there is nothing for Routine A2 to open
  later); post a brief note in `#distr-team-kb-log` (prefixed `[DRY RUN]` when
  DRY_RUN=true). Never post this to `#b-team-integrations`.
- Push fails: DM TONI_SLACK_ID with Status.md content and error details

Clean up: `rm -rf /tmp/dev-tools-integrations-marketplace-kb`
