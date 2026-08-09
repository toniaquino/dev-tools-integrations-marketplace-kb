# Universal Content Viewer (UCV) PRD

**Status:** In progress (original draft 2021, active development 2025–2026)
**PM:** Todd Willms
**Engineer lead:** Todd Willms
**Designer:** tonysmith-ux
**Last updated:** 2026-06-19
**Jira epics:** API-2454, API-2459, API-2677, API-2742

---

## Problem statement

Bynder customers integrate their Digital Asset Management platform with adjacent tools
(CMS, e-commerce, creative tools). These integrations need a consistent, embeddable
UI component to browse and select assets from Bynder without leaving the third-party tool.
The existing legacy compact view (/compact) is fragile, lacks modern feature parity
(AI search, Adaptive Video Streaming, correct permissions), and is built on deprecated
Shadow DOM architecture that must be removed.

## Customer segment

Developers and integration partners embedding Bynder asset selection into third-party
platforms. Enterprise customers who built custom integrations on the legacy compact view endpoint.

## Goals

- Provide a stable, evergreen embeddable asset picker (UCV) across all integration types
- Achieve feature parity with core DAM: AI search, video derivatives, user permissions
- Enable developers to configure the component (branding, filters, asset types) per integration context
- Complete migration off legacy Shadow DOM and legacy GraphQL service

## Non-goals

- Replacing the Bynder full DAM UI for primary asset management
- Building per-integration custom UIs — UCV is a shared component
- Webdam-specific features not on the shared roadmap

## Active workstreams (Q2 2026)

| Epic | Workstream | Status |
|---|---|---|
| API-2454 | Minor UX/UI gap fixes | 🟡 In progress |
| API-2459 | Mono-repo for UCV Regular/Lite | 🟡 In progress |
| API-2677 | Legacy /compact deprecation support | 🟡 In progress |
| API-2688 | Q2 bug fixes | 🟡 In progress |
| API-2614 | Decommission legacy ReasonML GraphQL service | 🟡 In progress |

## Planned workstreams (Backlog)

| Epic | Workstream |
|---|---|
| API-2742 | Telemetry and logging capabilities |
| API-2741 | GenAI POC for UCV |
| API-2737 | DAT preset folder organization in derivative menu |
| API-2738 | Define available image derivatives in dropdown |
| API-2739 | UCV respect user permissions for DAT Transform UI |
| API-2558 | Video derivatives availability in UCV |

## Requirements summary

### Must have (P0)
- AI search support (shipped Q3 2025 — API-2282)
- Adaptive Video Streaming link support (shipped Q3 2025 — API-2371)
- User permission enforcement matching DAM
- Migration path for existing /compact customers

### Should have (P1)
- Telemetry and logging for adoption tracking (API-2742)
- DAT preset folder organization in derivative menu (API-2737)
- GenAI integration POC (API-2741)

### Nice to have (P2)
- Custom branding per integration context
- Video derivatives in UCV dropdown (API-2558)
- Multi-collection support as asset source (API-2533)

## Success metrics

| Metric | Baseline | Target | How measured |
|---|---|---|---|
| Active UCV integrations | tonysmith-ux | tonysmith-ux | Analytics (PENDING tooling) |
| Legacy /compact endpoint traffic | tonysmith-ux | 0 at full deprecation | Server logs |
| Developer adoption | tonysmith-ux | tonysmith-ux | UCV telemetry (API-2742) |

## Dependencies

| Dependency | Owner | Status |
|---|---|---|
| UCV Gateway (GraphQL) | Engineering | 🟡 Decommission in progress (API-2614) |
| AI Search | Platform | ✅ Shipped (API-2282) |
| Analytics tooling | TBD | ⏸ PENDING — blocks metric tracking |

## Open questions

- /compact deprecation timeline: Owner: Todd Willms. Target: Q3 2026.
- Analytics tooling decision: Owner: TBD. Blocks metric tracking for API-2742.
- Figma files for current UCV designs: Owner: [Designer]. Needed for design/figma-index.md.
