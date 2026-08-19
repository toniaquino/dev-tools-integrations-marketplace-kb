# Routine 6 — Team Vault weekly status sync (Pass 1)

You are running headless in a GitHub Actions runner via `claude -p`. This prompt is
**self-contained**. Read it fully and execute it end to end. There is no human in the
loop during this run.

> **Provenance note (2026-08-19):** ported from
> `content-variations-delivery-performance-kb/.github/prompts/routine-6.md`, scoped to
> this repo's three squads and simplified: no digest-manifest batching (Routine 9 is
> not ported here — see `Governance.md` → "Routine 6" for why), no Todd/Bart
> cc-recipient logic (Todd Willms is a primary single-area owner here, not a
> cross-cutting recipient), and no per-owner multi-area batching (every owner here has
> exactly one area). Built ahead of real cross-squad demand, per Toni's explicit
> instruction, so the structure exists once a domain owner actually needs to skim
> status across all three squads at a glance.

This writes a **condensed, team-level `Status.md`** per squad
(`02 Teams/<Squad>/Status.md`) — separate from and simpler than the detailed
per-feature `Status.md` files Routine A already maintains under each squad's
`product-development/` tree. Do not confuse the two or conflate their content.

---

## Skills note — READ FIRST

Claude Code skills are **NOT available in this GitHub Actions runner**. Do not
invoke, load, or reference any skill. All logic is inlined below. **No MCP
connectors are configured** — talk to Slack and Jira through their REST APIs with
`curl` and the environment-variable tokens below. Do not call MCP tools.

---

## Environment & tooling

Available environment variables (same secrets already used by this repo's Routine A
workflows — see `Governance.md` → "Routine 6" for why no new secrets were added):

- `GH_PAT` — GitHub PAT for `toniaquino/dev-tools-integrations-marketplace-kb` (push + PR).
- `ATLASSIAN_API_TOKEN`, `ATLASSIAN_EMAIL` — Jira REST auth (basic auth).
- `SLACK_BOT_TOKEN` — Slack bot token (`chat:write`, `channels:history`). Bearer auth.

Access patterns (bash + `curl`):

- **Git / repo:** cloned at `/tmp/dev-tools-integrations-marketplace-kb` by the
  workflow (clone fresh if missing:
  `git clone https://toniaquino:$GH_PAT@github.com/toniaquino/dev-tools-integrations-marketplace-kb.git /tmp/dev-tools-integrations-marketplace-kb`).
  Push: `git -C /tmp/dev-tools-integrations-marketplace-kb push https://toniaquino:$GH_PAT@github.com/toniaquino/dev-tools-integrations-marketplace-kb.git <branch>`.
- **Slack read:** `conversations.history` / `conversations.replies`, header
  `Authorization: Bearer $SLACK_BOT_TOKEN`. Resolve channel IDs via
  `conversations.list` against the channel map below.
- **Slack write:** `chat.postMessage` to `#distr-team-kb-log` (tag the owner inline,
  `<@USER_ID>` — same channel this repo's Routine A already notifies to) and DM Toni
  directly (`conversations.open` with `U9ATXKJM6` then `chat.postMessage`).
- **Jira:** `GET https://bynder.atlassian.net/rest/api/3/search?jql=...`, basic auth
  `-u "$ATLASSIAN_EMAIL:$ATLASSIAN_API_TOKEN"`.
- **GitHub (push only):** pushes a branch per owner but does not open a PR — Routine
  6B opens it once that owner's thread confirms.

Confirm `"ok": true` (Slack) / HTTP 2xx before treating a call as successful.

---

## Global context

```
REPO:              github.com/toniaquino/dev-tools-integrations-marketplace-kb
SLACK_CHANNEL:     #distr-team-kb-log
TONI_SLACK_ID:     U9ATXKJM6
CLONE_PATH:        /tmp/dev-tools-integrations-marketplace-kb
MAIN_BRANCH:       main
```

Owner timezones (for Routine 6B's confirmation-deadline math and this routine's own
9am-local scheduling — **temporary hardcoded table**, same caveat as Routine A's:
switch to a live `users.info` lookup once the `users:read` Slack scope is granted):

```
Tony Smith  (UPQ9D0BFX):    America/New_York    (US Eastern)
Todd Willms (U01EHRXEBFE):  America/Los_Angeles (US Pacific)
Bas van Reeuwijk (U04H9D3H14K): Europe/Amsterdam (Amsterdam, CET)
```

### Source priority rules

Read from `Governance.md` → "Source priority rules" (Jira wins on delivery status;
Slack wins on decisions and blockers). Flag any conflict in the PR description rather
than resolving it silently.

### PR description format (used as the commit message body — Routine 6B reuses it verbatim as the eventual PR body)

```
## Routine 6 - Weekly Status Sync - [YYYY-MM-DD]

**Owner:** @[domain owner GitHub username]
**Area:** [Connectors | Integrations | Technology Partners]
**Files changed:** [list]

### What changed
[Bullet list of specific changes]

### Sources used
[Jira tickets, Slack channels referenced]

### Conflicts flagged
[Any source disagreements, or "None"]

### Staleness flags
[File past review due date, or "None"]
```

### Slack notification format

There is no PR yet at this point — link the branch's compare view:
`https://github.com/toniaquino/dev-tools-integrations-marketplace-kb/compare/main...<branch>`

```
@[domain owner] - weekly team-level status sync proposed for [Area], not yet a PR.

[1-line summary]. Conflicts: [flagged items or "none"]

Proposed changes: [compare URL]

Reply "👍" or "confirmed" in this thread to open the PR as-is.
Reply with any corrections — Routine 6B folds them in and opens the PR (36h later, or
sooner if triggered manually; silence at the deadline is treated as agreement).
Don't want to wait? Push directly to the branch above and open the PR yourself.
```

---

## Phase 1: read the ownership and channel map

Read `Governance.md` in the repo root. Parse the Ownership map and Channel map tables
to get, per area: domain owner, GitHub username (from that squad's own
`02 Teams/<Squad>/CLAUDE.md` team table — Governance.md does not carry usernames
itself), Slack ID, primary + additional channels.

If the channel map is entirely unpopulated, log a warning, DM Toni, and exit without
pushing branches.

## Phase 2: scan sources and update each area's Status.md

Process the three areas sequentially (Connectors, Integrations, Technology Partners).
For each:

- **Slack scan:** last 7 days across that area's primary + additional channels (see
  channel map). Extract status mentions, decision language ("we decided", "confirmed",
  "going with", "approved"), blocker language ("blocked", "at risk", "dependency on"),
  Jira ticket references.
- **Jira scan:** query every ticket referenced in Slack, current status + status
  changes in the last 7 days, on that squad's board (`INC` Connectors, `API`
  Integrations, board TBD for Technology Partners — if TBD, Jira-only signal is
  unavailable for that area, note it and proceed Slack-only).
- **Apply source priority rules.** Flag conflicts, never resolve silently.
- Read the current `02 Teams/<Squad>/Status.md` if it exists (baseline), or create it
  fresh using the format below if this is the area's first run.
- Update: status emoji + one-line summary, **Last updated** field (today), **Current
  state** (prepend new bullets, don't delete existing ones unless directly
  contradicted), **Blockers** (add new, mark resolved as "Resolved [date]" rather than
  deleting), **Source channels** (verify against the channel map).
- **Staleness check:** if `Last reviewed` is past `Review due`, prepend
  `> WARNING: This file is past its review due date. Last reviewed: [date]. Review due: [date].`

### Status.md format (inlined — use this exact template for a first-run file)

```markdown
# [Squad name]

**Status:** [emoji] [one-line summary]
**Last updated:** [YYYY-MM-DD]
**Last reviewed:** [YYYY-MM-DD]
**Review due:** [YYYY-MM-DD, +14 days from Last reviewed]
**Owner:** [domain owner name]
**Source channels:** [channel list]

## Current state
- [bullet]

## Blockers
- [bullet, or "None"]
```

Status emoji legend: 🟢 on track, 🟡 at risk, 🔴 blocked, ✅ shipped, ⏸ paused, 🔵 in
progress/discovery — match whichever legend that squad's own `02 Teams/<Squad>/CLAUDE.md`
declares if it differs from this list.

If no changes are detected for an area this run: skip it entirely (no branch, no
notification) and note it in the Phase 3 summary as "no changes."

## Phase 3: push branch and notify (once per owner — PR opens later, on confirmation)

For each area with changes:

- Branch: `status-sync/[squad-slug]-[YYYY-MM-DD]` off `main`.
- Commit the updated `Status.md` using the full PR write-up (per the format above) as
  the commit message — Routine 6B reads this back to open the PR later.
- Push.
- Do **not** open a PR yet.
- Post the Slack notification (format above) to `#distr-team-kb-log`, tagging the
  owner inline.

After all areas are processed, post a summary to `#distr-team-kb-log`:

```
Weekly team-level status sync complete — [YYYY-MM-DD]
Branches pushed (PRs pending confirmation): [N]
Areas with no changes: [list or "none"]
Branch list: [one line per branch: @owner — compare URL]
```

Then DM Toni (`U9ATXKJM6`):

```
Weekly status sync Pass 1 complete. [N] branches pushed (no PRs opened yet). Routine
6B runs 36 hours later to open each PR -- either once its thread confirms, or
automatically if 36 hours pass with no response (silence = agreement).
```

---

## Success criteria

- Ownership/channel map read; TBD areas logged and skipped (not fatal).
- One branch pushed per area with detected changes — no PR opened yet.
- `Status.md` updated with current state, blockers, staleness flags.
- Slack notification posted per area with changes; Pass 2 reminder DMed to Toni.

## Failure handling

- Jira API unavailable or board TBD: proceed Slack-only, note it in the PR
  description.
- Slack channel not found: log it, skip that channel for the scan (not the whole
  area), flag in the PR description.
- One area's processing fails: log the error, continue with the remaining areas, flag
  the failed area in the summary, DM Toni with the error.
- Push fails: log the error and DM Toni with the Status.md content and the error.
- Any uncaught fatal error: DM Toni with the routine name, the failed step, and the
  error text before exiting non-zero.
