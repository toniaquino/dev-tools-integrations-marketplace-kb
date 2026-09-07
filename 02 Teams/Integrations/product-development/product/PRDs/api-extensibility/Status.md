> ⚠️ **Overdue for human review.** Review due 2026-07-25 has passed (last reviewed 2026-06-27). Please have a human confirm this content is still accurate.

> ⚠️ **Overdue for human review.** Review due 2026-07-25 has passed (last reviewed 2026-06-27). Please have a human confirm this content is still accurate.

# API Extensibility

**Owner:** Todd Willms
**Status:** 🟡 Webhooks Part 1 remains blocked; Agentic SDK harness and Transformation Permissions work progressing
**Last updated:** 2026-08-18
**Last reviewed:** 2026-06-27
**Review due:** 2026-07-25
**Source channels:** #api-team, Jira API board

## Current state

- **Kong developer-portal CAB prep + "API-first middleware" positioning (new, 2026-08-27).** A skeleton/outline for the Kong/developer-portal Bynder Connect CAB update is being prepared, with Kevin Duque building the final deck from it (target: Sept 8 CAB session). Separately, Dom and Mike Mansell are shaping an "API-first middleware layer" position, which Dom has asked to be translated into a marketing narrative — intended to stay coherent with the portal-as-product/MCP-as-AI-hub framing raised in Todd Willms's 2026-08-25 1:1.
- Agentic SDK Implementation (API-2744): harness repo created (API-2858, done 2026-08-13) and harness set-up (API-2779) now In Progress; five SDK parity investigations (JS, Java, Python, PHP, C#) completed 2026-08-13 — epic itself still shows Backlog in Jira, which looks out of date given this activity
- Transformation Permissions epic (API-2747): follow-on ticket [FE] Enable Presets in DAT for UCV (API-2828) moved to Done as of 2026-08-17 (was in code review last week)
- React 19 migration progressing: UCV support (API-2838) moved to Merge status 2026-08-13; Integrations Hub support (API-2841) done 2026-08-13; release ticket API-2842 in code review as of 2026-08-17 and being validated via canary per #api-team
- Wiz vulnerability remediation for bynder-js-sdk (API-2859) completed 2026-08-17; remediation for other FE repos still pending owner follow-up per #api-team thread (2026-08-13)
- Webhooks Legacy Events Improvements Part 1 (API-2624) remains blocked, no movement since 2026-07-01 — still gating Part 2 (API-2670) and DAT Link Generated Event (API-2534). Owner assumed to have transferred to Efrain De Los Santos per the 2026-09-04 EM backfill below -- not independently confirmed in Jira.
- **Engineering org move, new (2026-09-04).** Wesley Christelis moving to lead API/Insomnia efforts. Efrain De Los Santos backfilling as EM for integrations -- becomes Tony Smith's new day-to-day engineering counterpart. The two already work together on Connectors, so this is a natural transition.

## Blockers

- **Webhooks Legacy Events Improvements Part 1 (API-2624)**: Blocking Webhooks Asset Legacy Events Part 2 (API-2670) and DAT Link Generated Event (API-2534). Owner: assumed transferred to Efrain De Los Santos following the 2026-09-04 EM backfill (Wesley Christelis moved to API/Insomnia) -- not independently confirmed in Jira, flag for correction if wrong. Status: Blocked as of 2026-07-01; requires external resolution.

## Commercial (Internal Only)

[No source link available]