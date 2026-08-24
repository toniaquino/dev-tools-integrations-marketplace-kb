# Connectors

**Status:** 🟡 At risk — needs attention
**Last updated:** 2026-08-24
**Last reviewed:** 2026-08-24
**Review due:** 2026-09-07
**Owner:** Tony Smith
**Source channels:** #team-connectors, #b-help-integrationshub (not found — see note), #b-team-integrations

## Current state
- Figma OAuth integration is at risk: the Studio team is deprecating Studio Gateway (`vbs-api-gateway`), which the Figma OAuth callback redirect currently depends on (`console.{env}.weadapt.digital`). Thread has run since 2026-08-20 with no resolution as of 2026-08-24; per Bill Keiffer, Tray (the integration hub's auth middleware) is not currently configured to act as a credential store/execution engine for this pattern, so this may require net-new work. (#b-team-integrations)
- Optimizely Connector v8.6.0 released by Geta (2026-08-17) — available to distribute to clients who purchased the connector. (#b-team-integrations)
- Canva integration: 4 customer tickets reported sudden connection loss (`"This Bynder domain isn't supported yet"`). Bas van Reeuwijk confirmed (2026-08-18) these should be routed to Canva Support since it's partner-supported, and he'll contact Canva directly. (#b-team-integrations)
- Active VNTANA (Michael Kors) connector work: INC-1430 (additional-asset import failing, in Code review), INC-1433 (duplicate assets on import, Done 2026-08-18), INC-1401 / INC-1323 (feature requests, To Do).
- Investigate creating a UCV Connector for Shopify (INC-1434, opened 2026-08-19, To Do).
- BEAST/SSTK storage migration: INC-1387, INC-1386, INC-1385, INC-1426, INC-1432 all shipped 2026-08-21; INC-1390 (data migration tooling from legacy storage to BEAST) still In Progress.
- Workfront embedded-metadata mapping bug flagged for Caesars Entertainment (ASSET-2974, owned by the Asset team, not on the INC board) — status "Waiting For Needs To Be Met" as of 2026-08-17. (#team-connectors)
- Free Pixelz integration question (School Outfitters) resolved by Bas van Reeuwijk with a documentation link (2026-08-19) — no further action.

## Blockers
- Figma OAuth callback redirect has no confirmed path forward once Studio Gateway is deprecated — cross-team dependency on the Studio team, unresolved as of 2026-08-24.

> Note: #b-help-integrationshub (this area's secondary channel per Governance.md) could not be resolved via Slack's channel list for this bot — it may not exist under that name, or the bot may not have access. Skipped per failure-handling rules; flagged here rather than blocking the rest of the scan.
