> ⚠️ **Overdue for human review.** Review due 2026-07-25 has passed (last reviewed 2026-06-27). Please have a human confirm this content is still accurate.

# API Extensibility

**Owner:** Todd Willms
**Status:** 🟡 Webhooks Part 1 remains blocked; Agentic SDK scope expanding with a new multi-language SDK epic; React 19 migration and Wiz remediation nearing completion
**Last updated:** 2026-08-25
**Last reviewed:** 2026-06-27
**Review due:** 2026-07-25
**Source channels:** #api-team, Jira API board

## Current state

- New epic API-2869 (Initial Multi-Language SDK Codebase & Public-Repo Fan-Out — Walking Skeleton) created 2026-08-19 with 12 scaffolding tasks defined across Python/Java/JS/C#/PHP SDKs (pagination, chunked upload, error mapping, CI gate); all still To Do — not yet reflected in feature-index.yaml
- Agentic SDK Implementation (API-2744) scope expanded to Asset API resumable-upload support across five languages (API-2770/2771/2772/2773, plus C# investigation API-2768) and per-language harness creation (API-2775/2776/2777/2778); Python harness (API-2776) now In Progress — epic itself still shows Backlog in Jira, which looks out of date given this activity
- Wiz vulnerability remediation completed for the two remaining flagged FE repos: bynder-compactview (API-2868, lodash CVE) done 2026-08-21 and ucv-chrome-extension (API-2867, postcss CVE) done 2026-08-19 — all FE repos flagged in prior weeks are now remediated
- React 19 migration: UCV support (API-2838) and Integrations Hub release (API-2842) both moved to Done; a full UCV migration PR (bynder-compactview #609, flagged as "a big one" per #api-team) is now tracked as API-2840 and in code review; new major UCV version release (API-2839) in progress, with two DATBuilderRevamped follow-on tasks queued (API-2855, API-2856)
- Webhooks Legacy Events Improvements Part 1 (API-2624) remains blocked and unassigned, no movement since 2026-07-01 — still gating Part 2 (API-2670) and DAT Link Generated Event (API-2534)

## Blockers

- **Webhooks Legacy Events Improvements Part 1 (API-2624)**: Blocking Webhooks Asset Legacy Events Part 2 (API-2670) and DAT Link Generated Event (API-2534). Owner: Unassigned in Jira — still to be confirmed. Status: Blocked as of 2026-07-01; requires external resolution.

## Commercial (Internal Only)

[No source link available]