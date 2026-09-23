# Integrations

**Status:** 🟡 At risk — strong delivery this week (harnessing nearly complete, Wiz vulnerabilities fixed, UCV React 19 migration ready to merge), but the SNS webhook SignatureVersion-2 blocker carries over unresolved.
**Last updated:** 2026-09-07
**Last reviewed:** 2026-08-31
**Review due:** 2026-09-14
**Owner:** Todd Willms
**Source channels:** #api-team, #b-team-integrations

## Current state
- Harnessing initiative nearly complete: PHP and Java harness creation shipped this week (API-2777, API-2778, both Done); UCV harness investigation moved to code review (API-2759); UCV Gateway harness investigation shipped (API-2787, Done). Python harness was already done (API-2776); resumable-upload tickets (API-2770/2771/2772/2773) unchanged this week.
- Agentic SDK OAuth endpoints shipped for both PHP and Python (API-2890, API-2885, Done).
- Wiz-flagged high-severity vulnerabilities fixed this week: bynder-compactview-superlight (postcss CVE-2026-45623, API-2892, Done) and ucv-chrome-extension (nanoid CVE-2026-73086, API-2891, Done). The same Wiz sweep (#api-team, 2026-09-04) also flagged bynder-js-sdk and bynder-wordpress, but no corresponding Jira ticket has surfaced yet for those two.
- UCV migration to React 19 (API-2840) is in Merge status — expected to land shortly.
- Electrolux Compact View Smartfilters load failure (API-2746, In Progress) — FE fix deployed to stage this week per #api-team.
- New FE bug: filter dropdown menus misalign in container display mode (API-2835, Code review).
- New tech-debt ticket: upgrade @bynder/design-system 7.13.0 → 8.14.0 in ucv-chrome-extension, requires TypeScript 5 (API-2893, To Do).
- Carried forward unchanged: isArchived filtering in code review (API-2352, API-2597) with an FE follow-up still to do (API-2610); SmartFilters performance improvements queued (API-2819, Backlog); GenAI Smartedit POC done (API-2854) with a related investigation still in progress (API-2741); Honeycomb tracing spike for webhooks/UCV logging still in progress (API-2823); Rabobank webhooks-UI migration (API-2852) and Integrations-team skills-repo setup (API-2887) still To Do.
- FYI from #api-team: company-wide production deployment freeze announced for Nov 23–30 and Dec 18–Jan 3 — worth factoring into Q4 release planning for this squad.

## Blockers
- SNS webhook SignatureVersion-2 (SHA-256) update is still blocked on DevOps permissions — unchanged since 2026-08-25 (source: Slack #b-team-integrations). Related tickets API-2864 and API-2889 remain To Do/Backlog in Jira, which still doesn't reflect a "blocked" state — same source conflict as the prior run, per Governance.md's priority rules (Slack wins on blockers). No new Slack activity on this thread in the last 7 days; carried forward from the 2026-08-31 baseline absent any contradicting signal.
