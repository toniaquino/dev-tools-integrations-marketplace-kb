# Integrations

**Status:** 🟡 At risk
**Last updated:** 2026-08-24
**Last reviewed:** 2026-08-24
**Review due:** 2026-09-07
**Owner:** Todd Willms
**Source channels:** #api-team, #b-team-integrations

## Current state
- Integrations Hub major version release shipped (API-2842, Done 2026-08-18) — version-bump PRs merged in `paramount` (#6776, #6797) and `integrations-tray-fe` (#140).
- UCV React 19 migration in progress: API-2840 "[FE] Migrate UCV to React 19" in Code review; large PR (`bynder-compactview` #609, opened 2026-08-21 by Artem Doba, ~95% mechanical changes). API-2839 "[FE] Release new major UCV version" is in Merge status.
- Colgate-Palmolive UCV Smartfilters bug (FSB-10885, In Progress) — fix staged for verification 2026-08-24 (intermittent repro confirmed by Dennis Ku on stage); a related but distinct Electrolux ticket (API-2746, To Do) was raised the same day and explicitly prioritized for this sprint per Tony Smith in Slack, since the customer is escalating.
- V4 Upload API SDK testing underway across JavaScript, Java, PHP, and Python (API-2811–API-2814); one issue already found and fixed in the Python SDK per Slack (2026-08-18).
- Wave 2 onboarding onto the Levante AI Acceleration Tracker dashboard: team confirmed the full list of owned GitHub repos (UCV, Integrations Hub, webhooks, SDKs, test repos) across 2026-08-19/20 to extend engineering-metrics coverage.
- Capacity note: Artem Doba (driving both the React 19 migration and the Smartfilters fix) is on PTO 2026-08-13 through 2026-08-30; Dennis Ku out 2026-08-27–28; Enver Yasar out 2026-08-31–09-07 (per weekly absence update, 2026-08-24).

## Blockers
- None currently blocking. At risk: Electrolux Smartfilters bug (API-2746) is customer-escalated and was verbally prioritized for this sprint in Slack (2026-08-24), but Jira still shows it at Minor priority — flagging as a source conflict per Governance.md (Jira status/priority is the system of record, but Slack carries the more current urgency signal here; not resolved silently).
