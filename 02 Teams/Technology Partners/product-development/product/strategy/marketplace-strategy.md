# Integrations Marketplace — Strategy

**Author:** Bas van Reeuwijk
**Audience:** Squad / Leadership
**Status:** Draft — seeded from Confluence 2026-06-19
**Last updated:** 2026-06-19
**Source:** https://bynder.atlassian.net/wiki/spaces/INTEGRATE/overview

---

## Bottom line

Bynder is shifting from merely having integrations to guaranteeing their quality and operational excellence. The strategy has two pillars: an engineering foundation (IAL) that makes partner onboarding faster and integrations more reliable, and a marketplace quality program (Certification) that makes this quality visible to customers and sales.

## Situation

Bynder's marketplace lists 100+ integrations. Partners build and maintain their own connectors. Bynder provides a technical validation process before listing. Support channels: #b-help-global-partnerships, partners@bynder.com. Integration types range from Bynder-owned (built in-house) to partner-built and community-built.

Current state:
- No visible quality signal on the marketplace — all integrations look the same
- Partner onboarding is manual and time-consuming (Bas runs 30-minute technical validation sessions per partner)
- Docs split across support.bynder.com and marketplace, creating duplication
- No standardised engineering layer for how integrations connect to Bynder internally

## Complication

As the marketplace grows, quality becomes a competitive differentiator. Customers increasingly evaluate integration breadth and reliability during procurement. Without quality signals, sales cannot confidently promote integrations. Without a standardised engineering layer, each new integration is a custom effort — not scalable.

## Resolution

**Short term (Q2/Q3 2026):**
- Ship IAL pilot adapter with feature flags by 2026-06-30
- Publish first port contract (Payments v1)
- Begin rolling out Integration Certification to existing partners

**Medium term:**
- Adapter SDK available for partners to self-serve integration development
- Blue Checkmark visible on marketplace; certified integrations rank higher
- Documentation fully migrated from support.bynder.com to marketplace

**Long term:**
- Partner onboarding time reduced by 50%
- Core adapter availability above 99.9%
- Marketplace becomes a curated ecosystem, not just a directory

## Alternatives considered

- Status quo (no quality signalling, manual onboarding): rejected — does not scale; weakens Bynder's competitive position as DAM market matures
- Build a separate partner portal: deferred — API-first is preferred; a portal is a Phase 2 consideration
- Own and build all integrations in-house: not viable — partner ecosystem model is the right approach for scale

## What we need to decide

| Decision | Owner | Target date |
|---|---|---|
| Engineering lead for IAL pilot adapter | Bas van Reeuwijk | [TO COMPLETE] |
| Q3 target number of certified integrations | Bas van Reeuwijk | [TO COMPLETE] |
| Whether IAL Adapter SDK is exposed externally to partners | Bas van Reeuwijk | [TO COMPLETE] |
| Analytics tooling for marketplace metrics | TBD (Bynder-level decision) | TBD |

## Implications

- Engineering team must prioritise IAL pilot before end of Q2 (2026-06-30 target)
- Partnership team needs to proactively reach out to top partners about certification
- CS team benefits from certified integrations via clearer documentation and faster issue diagnosis
- Sales gains a tangible differentiator: "certified integrations"

## Open questions

- What is the current partner onboarding baseline time (to measure the -50% target)?
- How many partners are in the certification pipeline as of today?
- Which integrations are in scope for the IAL pilot?
