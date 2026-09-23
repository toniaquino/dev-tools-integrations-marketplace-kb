> ⚠️ **Overdue for human review.** Review due 2026-07-25 has passed (last reviewed 2026-06-27). Please have a human confirm this content is still accurate.

# API Extensibility

**Owner:** Todd Willms
**Status:** 🟡 Webhooks Part 1 remains blocked; Agentic SDK harnessing and new Asset API Integration work accelerating; Wiz security remediation nearly complete
**Last updated:** 2026-09-15
**Last reviewed:** 2026-06-27
**Review due:** 2026-07-25
**Source channels:** #api-team, Jira API board

## Current state

- **Agentic SDK Implementation (API-2744) harnessing sprint, 2026-09-08 to 09-14.** All five language harnesses (Python, PHP, C#, Java, JS/TS) built and scaffolded, plus Python OAuth 2.0 endpoints (API-2885) shipped -- epic itself still shows Backlog in Jira despite this volume of work, extending the stale-status issue flagged last week.
- **New work stream surfaced: Asset API Integration (API-2869), not yet in feature-index.yaml.** Resumable-upload conformance work spans Python/PHP/Java/JavaScript/TypeScript, with roughly 14 sub-features (draft asset create/trash/publish, chunked upload, retry/backoff, session persistence) and a QA pass assigned to Enver Yasar (API-2808).
- Wiz security remediation: bynder-sfcc's last 3 open Highs cleared, PR up for review (API-2912, bynder-sfcc#10) -- 2 Snyk issues remain To Do (python-integrations-webhooks-lib, bynder-js-sdk). Parent epic API-2903 still shows Backlog in Jira despite this progress.
- Electrolux Compact View Smartfilters bug (API-2746 / FSB-11845) still unresolved as of 2026-09-08 -- GraphQL error persists on stage ("Argument 'filter' is not defined on field 'filters'"); owner Alex Hong.
- Two Honeycomb/UCV-telemetry epics now active in parallel -- API-2742 (tracked in feature-index) and new API-2896 "Implement Honeycomb for UCV" (untracked) -- both have Honeycomb child tasks in progress under Nikhil Potlapally; needs Todd to confirm whether these should merge or stay separate.

## Blockers

- **Webhooks Legacy Events Improvements Part 1 (API-2624)**: Blocking Webhooks Asset Legacy Events Part 2 (API-2670) and DAT Link Generated Event (API-2534). Owner: assumed transferred to Efrain De Los Santos following the 2026-09-04 EM backfill (Wesley Christelis moved to API/Insomnia) -- still not independently confirmed in Jira (assignee field still empty), flag for correction if wrong. Status: Blocked; Jira record last touched 2026-09-10 with no status change; requires external resolution.

## Commercial (Internal Only)

[No source link available]
