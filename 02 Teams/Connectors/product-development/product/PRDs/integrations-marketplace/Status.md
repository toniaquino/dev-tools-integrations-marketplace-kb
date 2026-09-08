> ⚠️ **Overdue for human review.** Review due date (2026-08-18) has passed with no
> recorded human review since 2026-07-21. Automated weekly synthesis updates do not
> count as a review -- please have a human confirm this file.

# Integrations Marketplace

**Owner:** Tony Smith
**Status:** 🟡 Electrolux integration bug remains an open critical blocker (workaround holding, no change this week); SSTK/BEAST migration work continued with several items shipped; Wiz vulnerability scan findings (36) on connector-code-storage in code review; Claude-in-Tray research spike completed
**Last updated:** 2026-09-08
**Last reviewed:** 2026-07-21
**Review due:** 2026-08-18
**Source channels:** #team-connectors (accessible this run via the hardcoded channel ID); #b-help-integrationshub returned `not_in_channel` this run -- bot still not a member, same as prior weeks; Jira board INC.

## Current state

- **Getty sync-latency bug fixed, new (2026-09-07):** "Sync takes longer than 2 hours" (INC-1436, under Technical Debt & Maintenance epic INC-451) shipped.
- **SSTK/BEAST migration progressed, new (2026-09-04):** BEAST calls converted to the prod environment and BEAST migration performed for current SSTK instances (INC-1389, INC-1391), both under the SSTK epic (INC-1341 -- still not tracked in feature-index.yaml); metadata-map extraction for client updates also completed this week (INC-1438).
- **Michael Kors / VNTANA asset-duplication bug resolved, new (2026-09-03):** iHub connector duplicating assets on import fixed (INC-1433, under General Bugs & Support - Q3 2026, INC-1336) -- likely the same issue flagged as INC-1430 in last week's notes, though the ticket keys differ and this has not been confirmed. A separate VNTANA feature-request research item from Michael Kors remains open (INC-1323, To Do).
- **Claude-in-Tray research spike completed, status change (2026-09-02):** the evaluation opened last week (INC-1421, under INC-1342) moved from To Do to Done.
- **Security: Wiz vulnerability scan in review, new (2026-09-02):** 36 findings on connector-code-storage are in code review (INC-1441, owner MK de Gucena).
- Also this week, not yet reflected above: Box Integration task closed (INC-1440, 2026-09-01); a Lee Company iStock term-override request opened (INC-1442, To Do, unassigned); Vimeo epic INC-1337 appears retitled from "Vimeo POC - Q3 2026" (per feature-index.yaml) to "Vimeo Architectural Diagrams - Q3 2026" in Jira -- status unchanged (To Do), flagged as a naming gap only, not a status change.
- In #team-connectors, MK de Gucena asked where previously-streamed Tray data lives for the Task Usage reporting research (referencing INC-1343) -- unanswered in-thread as of this scan -- and separately shared a multi-agent AI skill for generating technical docs from Tray project exports.

## Blockers

- 🔴 Electrolux integration bug is a critical blocker limiting CX/Omnichannel feature use, carried over, no change this week -- workaround holding, escalate only if it fails.

## Commercial (Internal Only)
