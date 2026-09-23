> ⚠️ **Overdue for human review.** Review due 2026-07-25 has passed (last reviewed 2026-06-27). Please have a human confirm this content is still accurate.

# API Extensibility

**Owner:** Todd Willms
**Status:** 🟡 Webhooks Part 1 remains blocked; Agentic SDK OAuth/harness work advancing, Electrolux smartfilters bug under active investigation
**Last updated:** 2026-09-08
**Last reviewed:** 2026-06-27
**Review due:** 2026-07-25
**Source channels:** #api-team, Jira API board

## Current state

- **Electrolux Compact View Smartfilters bug (API-2746), new (2026-09-02 to 09-04).** Root cause traced to the gateway failing to resolve `metapropertyFilters` in the GraphQL response while other fields (tags, count) return fine; BE fix owned by Alex Hong still in progress. FE graceful-fallback fix (bynder-compactview PR #618) deployed to stage 2026-09-04, pending Tony Smith verification.
- **Wiz high-severity vulnerability sweep, new (2026-09-03 to 09-04).** New findings flagged across ucv-chrome-extension, bynder-compactview-superlight, bynder-js-sdk, and bynder-wordpress; postcss CVE (API-2892) and nanoid CVE (API-2891) fixed 2026-09-04 for the first two repos. bynder-js-sdk and bynder-wordpress remediation still pending owner follow-up (open since 2026-08-13).
- **Agentic SDK Implementation (API-2744) progressing, new (2026-09-01 to 09-03).** PHP and Java harness set-up (API-2777, API-2778) and PHP/Python OAuth endpoint implementation (API-2890, API-2885) all completed this week — epic itself still shows Backlog in Jira, increasingly out of date given this sustained activity (also flagged last update).
- **Engineering org move (2026-09-04).** Wesley Christelis moving to lead API/Insomnia efforts. Efrain De Los Santos backfilling as EM for integrations -- becomes Tony Smith's new day-to-day engineering counterpart. The two already work together on Connectors, so this is a natural transition.
- React 19 migration: UCV support (API-2840) moved to Merge status 2026-09-02; Integrations Hub support and the release ticket were previously completed/in canary review as of 2026-08-17.

## Blockers

- **Webhooks Legacy Events Improvements Part 1 (API-2624)**: Blocking Webhooks Asset Legacy Events Part 2 (API-2670) and DAT Link Generated Event (API-2534). Owner: assumed transferred to Efrain De Los Santos following the 2026-09-04 EM backfill (Wesley Christelis moved to API/Insomnia) -- not independently confirmed in Jira, flag for correction if wrong. Status: Blocked as of 2026-07-01, no movement this week; requires external resolution.

## Commercial (Internal Only)

[No source link available]