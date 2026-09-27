# Integrations — Decisions

> **Seeded 2026-09-27** from `content-variations-delivery-performance-kb`'s archived
> copy (that repo's copy is now a frozen historical snapshot — see its ARCHIVED
> banner). This is the live copy going forward; edit here, not there. Migrated late
> — the 2026-08-19 Connectors/Technology Partners Decisions.md seed missed this file.

## Prioritize Braze i-Hub into Q3.1
**Date:** 2026-06-19
**Owner:** Tony Smith
**Status:** Decided
**Context:** Braze partnership and GTM momentum (Dom) warranted moving the integration forward.
**Decision:** Move the Braze i-Hub integration up to Q3.1 priority.
**Implications:** Data-mapping research (INC-1315) becomes the gating dependency.
**Source:** Jira INC-1239; Q3 2026 Roadmap master section 5.

## Contentful integration on hold
**Date:** 2026-06-19
**Owner:** Tony Smith / Dom
**Status:** Decided
**Context:** Salesforce's acquisition of Contentful created uncertainty around the integration's direction.
**Decision:** Hold the Contentful integration pending the Salesforce acquisition outcome.
**Implications:** Deprioritized for Q3; revisit once the acquisition direction is clear.
**Source:** Q3 2026 Roadmap master section 5 (Integrations open decisions).

## Validate POC (UCV GenAI) objective closed
**Date:** 2026-07-15
**Owner:** Tony Smith / Todd Willms
**Status:** Decided
**Context:** The "Validate POC" ticket's scope was ambiguous going in.
**Decision:** Tony Smith and Todd Willms agreed the ticket's job was only to scope the GenAI/UCV question, not implement it. Marked 100% complete. Tony Smith to create a new ticket to track actual GenAI/UCV implementation work.
**Implications:** Decouples scoping from implementation tracking; implementation work is not yet ticketed.
**Source:** Integrations & Connectors ToT, 2026-07-15 (transcript ~00:11:12). Toni Aquino did not attend; reviewed via Gemini notes/transcript.

## GenAI/UCV workflow: PRD before epics
**Date:** 2026-07-15
**Owner:** Tony Smith / Todd Willms
**Status:** Decided
**Context:** GenAI/UCV work risked jumping straight to epics without a defined scope. Framed explicitly as an upsell opportunity given UCV's existing customer embed footprint. Dennis Ku confirmed technical feasibility (if a feature exists in the portal, no blocker to UCV).
**Decision:** No epic will be created for GenAI/UCV directly. A robust PRD (Confluence page or Google Doc is acceptable) must define scope first; the PRD then breaks into multiple epics/milestones.
**Implications:** Delays epic creation until the PRD lands; positions GenAI/UCV as a commercial upsell motion, not just an engineering task.
**Source:** Integrations & Connectors ToT, 2026-07-15 (transcript ~00:12:04-00:15:21). Toni Aquino did not attend; reviewed via Gemini notes/transcript.

## UCV telemetry investigation kicked off
**Date:** 2026-07-15
**Owner:** Todd Willms / Tony Smith
**Status:** Decided
**Context:** Structured telemetry for UCV has not started. Deciding what to capture (global attributes, e.g. which integrator is embedding, user agent) is the hard part, not implementation.
**Decision:** Working session scheduled Monday 2026-07-20 (Todd Willms, Dennis Ku, Tony Smith, Wesley Christelis) to start a Confluence page, building on Tony Smith's preliminary property list already in Jira.
**Implications:** Telemetry scoping becomes a tracked working session with a named owner group and start date.
**Source:** Integrations & Connectors ToT, 2026-07-15 (transcript ~00:16:19-00:18:47). Toni Aquino did not attend; reviewed via Gemini notes/transcript.

## ING webhook/CDN race condition — short-term fix approved
**Date:** 2026-07-15
**Owner:** Tony Smith / Dennis Ku
**Status:** Decided
**Context:** Root cause: the legacy asset media updated event reaches ING before Bynder's own CDN invalidation completes, causing stale-version delivery. A global delay was rejected due to prior Kafka backlog/outage risk.
**Decision:** Approved a 1-second (up to 3s pending log validation) non-blocking delay via feature split, scoped to ACI clients, ING first. Staging validation required before rollout.
**Implications:** Fix is scoped and flagged, not global; requires staging validation before any wider rollout beyond ING/ACI clients.
**Source:** Internal - Discuss ING Webhook/CDN Invalidation Issue, 2026-07-15 (transcript ~00:18:21-00:27:47). Toni Aquino did not attend; reviewed via Gemini notes/transcript.
