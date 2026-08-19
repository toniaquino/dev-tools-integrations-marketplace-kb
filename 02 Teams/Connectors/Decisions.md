# Connectors — Decisions

> **Seeded 2026-08-19** from `content-variations-delivery-performance-kb`'s archived
> copy (that repo's copy is now a frozen historical snapshot — see its ARCHIVED
> banner). This is the live copy going forward; edit here, not there.

## Tray storage-node deprecation deescalated
**Date:** 2026-06-19
**Owner:** Tony Smith
**Status:** Decided
**Context:** A prior plan treated June 30 as a hard storage-node deprecation deadline for Tray.
**Decision:** Deescalate — June 30 is pagination enforcement only, not a hard cutover.
**Implications:** Removes a false deadline; BEAST (INC-1241) remains the Tray storage framework. The OAuth → Salesforce migration (BODEV-5680) is a Business Operations Jira project item, not owned by any DISTR team — not tracked in this KB.
**Source:** Q3 2026 Roadmap master section 5 (Integrations & Connectors).

## Create the Connectors Q3 objective set
**Date:** 2026-06-19
**Owner:** Tony Smith
**Status:** Decided
**Context:** No formal Q3 objectives, fixVersions, or PI keys exist for Connectors.
**Decision:** Tony to author the Connectors Q3 objective set.
**Implications:** Needed before deliverable-level tracking (e.g. the Akeneo connector) can begin.
**Source:** Q3 2026 Roadmap master section 8 (open decisions).

## Chrome extension commitments require architecture sign-off
**Date:** 2026-07-15
**Owner:** Todd Willms
**Status:** Decided
**Context:** Chrome extension work (currently MK de Gucena's exploration) risked becoming an ad hoc, customer-specific commitment. The ING webhook/CDN incident (see 02 Teams/Integrations/Decisions.md, 2026-07-15) was cited as the cautionary precedent for ad hoc, customer-specific commitments becoming unsupportable technical debt.
**Decision:** Any Chrome extension work must be vetted by Dennis Ku / the architecture team before development commitment.
**Implications:** Adds an architecture-review gate before any new Chrome extension commitment; applies to future exploration, not just MK de Gucena's current work.
**Source:** Agile Refresh, 2026-07-15 (transcript ~00:28:19-00:29:28). Toni Aquino did not attend; reviewed via Gemini notes/transcript.
