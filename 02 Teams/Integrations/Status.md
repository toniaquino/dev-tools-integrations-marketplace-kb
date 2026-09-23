# Integrations

**Status:** 🟡 At risk — Webhooks Legacy Events Part 1 still blocked; Agentic SDK harness build progressing fast across 5 languages
**Last updated:** 2026-09-14
**Last reviewed:** 2026-09-14
**Review due:** 2026-09-28
**Owner:** Todd Willms
**Source channels:** #api-team, #b-team-integrations (shared); Jira board API

## Current state

- **Agentic SDK Implementation (API-2744) harness build active across all 5 target languages.** Harness repos (Python, PHP, C#, Java) and their SDK-parity investigations all completed; JS and TypeScript harnessing also done. Initial scaffold tickets (F10 Java, F11 JS, F12 C#, F13 PHP) marked Done alongside the Python reference track (F1 monorepo scaffold, F4 OAuth base client, F8 idiomatic error mapping) — a large, mostly same-day (2026-09-14) batch of movement, worth confirming with Todd whether this reflects genuine same-week completion or a bulk Jira status sync. Asset-API "create/trash a Draft asset" work (F14, API-2768/API-2917) now In Progress; the next milestone chunk (F15 publish, F16–F20 resumable upload/retry/progress) and per-language resumable-upload rollout tickets are queued To Do.
- **Electrolux Compact View Smartfilters (API-2746):** per the #api-team thread, backend fix deployed to production 2026-09-14 after FE/BE validation on stage this week (429-error root cause on large-taxonomy portals). **Conflict flag:** Jira still shows API-2746 as In Progress (last synced 2026-09-08, before the prod deploy) — Jira source-of-truth is stale relative to this Slack signal; treat as likely resolved pending Jira catching up.
- Security remediation cleared this week: Wiz High findings on `bynder-sfcc` fixed via draft PR (API-2912, per #api-team 2026-09-13) — closed out the team's only open Wiz Highs on that repo; Snyk issues addressed on `python-integrations-webhooks-lib` and `bynder-wordpress` (both Done). `bynder-js-sdk` Wiz dependency bump (API-2908) shipped as part of the v2.5.8 release (2026-09-14, per GitHub notifications in #api-team), which also carried the fix for the JS-SDK opaque-TypeError bug (API-2895) reported and fixed within the same week.
- React 19/UCV migration and Honeycomb observability build-out (tracing spans, board creation, NLS API-usage tracing) both actively In Progress this week.
- API-2835 ([FE] filter-dropdown misalignment) flagged in #api-team as ready for stage validation ahead of Monday.
- **Slack outside the above was routine team-ops** (weekly absence updates, an internal Claude-credit-request flow question) — no additional PM-level decisions surfaced.

## Blockers

- **Webhooks Legacy Events Improvements Part 1 (API-2624):** Blocked in Jira, last touched 2026-09-10. Continues to gate Webhooks Asset Legacy Events Part 2 (API-2670) and DAT Link Generated Event (API-2534); no Slack discussion of this ticket surfaced in this week's #api-team scan.
