# Integrations Marketplace PRD

**Status:** Draft — stub seeded 2026-06-19, complete with Bas van Reeuwijk
**PM:** Bas van Reeuwijk
**Engineer lead:** [TO COMPLETE]
**Designer:** [TO COMPLETE]
**Last updated:** 2026-06-19
**Jira epic:** [TO COMPLETE — no Jira board]
**Confluence:** https://bynder.atlassian.net/wiki/spaces/INTEGRATE/overview

---

## Problem statement

Bynder's marketplace lists 100+ integrations built by technology partners, but customers and sales have low confidence in integration quality. There is no visible signal distinguishing high-quality, well-supported integrations from unmaintained ones. Partner onboarding is slow and manually intensive, reducing the pace at which new integrations reach the marketplace.

## Customer segment

Enterprise and mid-market DAM buyers evaluating Bynder as a system of record. Integration breadth and reliability are evaluated during procurement. Also: technology partners building connectors to Bynder who need a clear, efficient path to marketplace listing.

## Goals

- Increase customer confidence via visible quality signals (Integration Certification Blue Checkmark)
- Reduce partner onboarding time by 50% via the Integration Abstraction Layer (IAL)
- Achieve greater than 99.9% availability on core integration adapters
- Centralise integration documentation on the marketplace

## Non-goals

- Custom UIs for partner management (API-first approach)
- Long-term ETL/analytics pipelines (data platform)
- Owning support for partner-built integrations (partners own their support)

## Solution

Three parallel workstreams:

**1. Integration Certification Program** — quality certification for marketplace listings. Partners meeting Bynder's requirements earn a Blue Checkmark, appear higher in search, and become prioritised referrals.

**2. Integration Abstraction Layer (IAL)** — unified engineering layer standardising how integrations connect to Bynder. Domain ports and adapters architecture, centralised auth/retries/observability. Reduces partner onboarding complexity.

**3. Marketplace documentation migration** — moving partner connector docs from support.bynder.com to marketplace listing pages.

## Requirements

### Must have (P0)
- Certification: partners can apply, Bynder reviews, certified integrations earn Blue Checkmark
- IAL: pilot adapter live with feature flags by 2026-06-30
- IAL: port contract published

### Should have (P1)
- IAL: Adapter SDK with auth, retries, tracing, test utilities
- Certified integrations ranked higher in marketplace search
- Documentation migration complete for major partner integrations

### Nice to have (P2)
- Partner self-service dashboard for certification status
- Automated technical validation tooling

## Success metrics

| Metric | Baseline | Target | How measured |
|---|---|---|---|
| Partner onboarding time | [TO COMPLETE] | -50% | Internal measurement |
| Core adapter availability | [TO COMPLETE] | >99.9% | Observability dashboards |
| MTTR | [TO COMPLETE] | <15 minutes | Incident tooling |
| Certified integrations count | 0 | [TO COMPLETE] | Marketplace certification tracker |

## Dependencies

| Dependency | Owner | Status |
|---|---|---|
| Engineering lead for IAL pilot adapter | [TO COMPLETE] | 🟡 In progress |
| Partnership team for certification outreach | partners@bynder.com | 🟢 Active |
| Marketplace platform for Blue Checkmark UI | [TO COMPLETE] | [TO COMPLETE] |

## Open questions

- Who is engineering lead for IAL? Owner: Bas. Target: [TO COMPLETE]
- Target number of certified integrations for Q3? Owner: Bas. Target: [TO COMPLETE]
- Will IAL be exposed as an external partner SDK? Owner: Bas. Target: [TO COMPLETE]

## Alternatives considered

Status quo (manual onboarding, no quality signalling): rejected — does not scale and weakens competitive position. Separate partner portal: deferred in favour of API-first approach.
