# Integrations Marketplace

> ⚠️ **Overdue for human review.** Last reviewed 2026-07-21; review was due 2026-08-18. Content below continues to be refreshed weekly by the synthesis routine, but needs a human pass to confirm accuracy.

**Owner:** Tony Smith
**Status:** 🟡 Shipping continued at pace (BEAST/SSTK sub-features, VNTANA asset-duplication fix), but a new external dependency risk surfaced this week -- see Blockers.
**Last updated:** 2026-08-25
**Last reviewed:** 2026-07-21
**Review due:** 2026-08-18
**Source channels:** #team-connectors (accessible this run via the hardcoded channel ID) and #b-help-integrationshub (`not_in_channel` again this run — bot still not a member, same as prior weeks); Jira board INC.

## Current state

- Michael Kors / VNTANA: new "connector duplicating assets on import" bug (INC-1433) opened and shipped same day; the separate "additional asset is failing" bug (INC-1430) advanced from To Do to Code review; feature-request items (INC-1401, INC-1323) remain To Do.
- SSTK / BEAST Q3 2026 build (epic INC-1341, still not tracked in feature-index.yaml): five sub-features shipped this week -- BEAST storage-activation flow, Sync Controller record fetch, and uploader-flow record adds (INC-1385, INC-1386, INC-1387), connector user-agent header update (INC-1426), and sync queueLock (INC-1432); data-migration tooling from legacy storage (INC-1390) in progress.
- New investigation opened: UCV Connector for Shopify (INC-1434, To Do) -- not yet scoped or added to feature-index.yaml.
- Squad channel flagged a Bynder Asset-API bug (ASSET-2974, owned by the Asset team, tracked outside board INC) blocking embedded-metadata mapping on Workspace upload for Workfront customer Caesars Entertainment.
- No epic-level status changes this week for features already tracked in feature-index.yaml (Zyng, Unsplash, Vimeo POC, Braze POC all unchanged); no epics shipped this week -- feature launch completeness check (Phase 2c) has nothing to flag.

## Blockers

- Embedded metadata mapping for Workfront (Caesars Entertainment): depends on a fix from the Asset team to the new asset API; blocks confirming this Workspace-upload workflow as complete. Owner: Asset team -- no named individual surfaced in the Slack thread; flagged for Tony Smith to confirm an escalation contact. Status: open, tracked in ASSET-2974 (Asset team's board, not INC).

## Commercial (Internal Only)
