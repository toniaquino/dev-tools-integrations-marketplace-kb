> ⚠️ **Overdue for human review.** Review due 2026-07-25 has passed (last reviewed 2026-06-27). Please have a human confirm this content is still accurate.

# API Extensibility

**Owner:** Todd Willms
**Status:** 🟡 Webhooks Part 1 remains blocked; React 19 migration, Agentic SDK fan-out, and an Electrolux customer fix progressing
**Last updated:** 2026-09-22
**Last reviewed:** 2026-06-27
**Review due:** 2026-07-25
**Source channels:** #api-team, Jira API board

## Current state

- **Staffing change (new, 2026-09-19).** Artem Doba (Senior FE Engineer) is transitioning off Integrations frontend repos to the Portal team; requested a handover doc covering caveats in the integrations frontend repos before the transition completes.
- **Engineering hygiene, new this week.** React 19 migration continues: bynder-compactview merge conflicts fixed and PR #609 on stage for testing (2026-09-17), harness update PR #619 raised, and a new ticket to upgrade ucv-chrome-extension to React 19 opened (API-2967, 2026-09-22, To Do, Dennis Ku). Separately, Snyk high-vulnerability remediation tickets under API-2903 closed (API-2904, API-2907, 2026-09-16), continuing the vulnerability-remediation thread from the 2026-08-17 Wiz work.
- **Electrolux customer issue, new this week.** Compact View Smartfilters failing to load (API-2746, in Merge as of 2026-09-21). A brand-guidelines-prod release was rolled out 2026-09-16 aimed at this, with two follow-up PRs raised to bump UCV in the guidelines-frontend and paramount repos.
- Agentic SDK / Multi-Language SDK fan-out (API-2869, feeds Agentic SDK Implementation API-2744): Asset API F14 (create + trash a Draft asset) delivered across all SDKs (API-2768, Done 2026-09-21); OpenAPI spec retrieval from Backstage YAML done (API-2924); fan-out task API-2919 in progress. Epic API-2744 itself still shows Backlog in Jira -- same discrepancy as noted in the prior update.
- UCV Add Telemetry and Logging Capabilities (API-2742) moved to In Progress in Jira (2026-09-17, spike API-2823 done) -- feature-index status updated from 🔵 Planning to 🟡 In progress accordingly.
- Webhooks Legacy Events Improvements Part 1 (API-2624) remains blocked -- touched in Jira 2026-09-10 but status unchanged, still gating Part 2 (API-2670) and DAT Link Generated Event (API-2534). Owner assumed to have transferred to Efrain De Los Santos per the 2026-09-04 EM backfill -- not independently confirmed in Jira.

## Blockers

- **Webhooks Legacy Events Improvements Part 1 (API-2624)**: Blocking Webhooks Asset Legacy Events Part 2 (API-2670) and DAT Link Generated Event (API-2534). Owner: assumed transferred to Efrain De Los Santos following the 2026-09-04 EM backfill (Wesley Christelis moved to API/Insomnia) -- not independently confirmed in Jira, flag for correction if wrong. Status: Blocked, last touched in Jira 2026-09-10; requires external resolution.

## Commercial (Internal Only)

[No source link available]