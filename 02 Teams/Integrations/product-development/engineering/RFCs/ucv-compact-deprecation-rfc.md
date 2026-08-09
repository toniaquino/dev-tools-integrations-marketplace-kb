# STUB: Content to be completed — seeded 2026-06-19
# Source: Jira epic API-2677 (In Progress as of 2026-06-19)
# Format: see .claude/writing-guides/rfc-guide.md

# RFC: Legacy UCV Compact View Deprecation -- 2026-Q2

**Author:** [TO COMPLETE — engineering lead for API-2677]
**Status:** In review
**Jira epic:** API-2677
**Review by:** tonysmith-ux
**Reviewers:** Todd Willms, Todd Willms, [others]

---

## Summary

[TO COMPLETE — define the deprecation path for the legacy /compact endpoint and
Shadow DOM-based UCV, including partner migration timeline, fallback strategy,
and hard sunset date]

## Motivation

[TO COMPLETE — describe the current /compact endpoint burden: fragile Shadow DOM
architecture, feature gap vs. UCV (no AI search, no correct permissions, no Adaptive
Video Streaming), maintenance cost, and security/technical debt implications]

## Scope of impact

- **Partners affected:** [TO COMPLETE — all customers currently using /compact embed URL]
- **Integration types:** CMS plugins, custom integrations, connector apps
- **Traffic baseline:** [TO COMPLETE — current /compact endpoint traffic]

## Proposal

[TO COMPLETE — describe the deprecation plan:
1. Deprecation notice period (recommended: 6 months minimum)
2. Migration guide to UCV Regular/Lite
3. Redirect or stub behavior during wind-down
4. Hard shutdown date and process]

## Alternatives considered

| Alternative | Why rejected |
|---|---|
| Keep /compact indefinitely | Unsustainable maintenance cost; blocks Shadow DOM removal |
| Auto-migrate /compact traffic to UCV | [TO COMPLETE — compatibility risks] |

## Impact

| Area | Impact |
|---|---|
| Partners | Requires migration action — communication plan needed |
| Performance | /compact removal reduces server load |
| Security | tonysmith-ux |
| UCV scope | Must have feature parity before sunset (AI search ✅, permissions ✅) |

## Migration checklist

- [ ] Feature parity verified (see ucv-prd.md)
- [ ] Migration guide published to developer docs
- [ ] Deprecation notice sent to affected partners
- [ ] Redirect behavior defined
- [ ] Sunset date confirmed with Todd Willms / Todd Willms

## Open questions

- Hard sunset date: Owner: Todd Willms. Target: Q3 2026 (to be confirmed).
- How many active /compact customers still require migration? Owner: engineering.

## Decision

[TO COMPLETE — update when RFC is resolved]
