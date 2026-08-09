# STUB: Content to be completed — seeded 2026-06-19
# Source: Jira epic API-2614 (In Progress as of 2026-06-19)
# Format: see .claude/writing-guides/rfc-guide.md

# RFC: Decommission ReasonML GraphQL Service -- 2026-Q2

**Author:** [TO COMPLETE — engineering lead for API-2614]
**Status:** In review
**Jira epic:** API-2614
**Review by:** tonysmith-ux
**Reviewers:** Todd Willms, [others]

---

## Summary

[TO COMPLETE — decommission the legacy ReasonML-based GraphQL service (UCV Gateway)
that backs the current /compact endpoint and parts of UCV, replacing all consumers
with a modern equivalent or direct API calls]

## Motivation

[TO COMPLETE — describe the ReasonML GraphQL service burden: ReasonML is a deprecated
language choice for this context, the service is the main remaining blocker for
/compact deprecation, it has limited maintainability as team expertise in ReasonML
erodes, and it creates a dependency bottleneck for UCV feature development]

## Current consumers

| Consumer | Status |
|---|---|
| /compact endpoint | Blocking decommission — see API-2677 |
| UCV Regular | [TO COMPLETE — partially migrated or still dependent?] |
| UCV Lite | tonysmith-ux |
| Other services | [TO COMPLETE — audit required] |

## Proposal

[TO COMPLETE — describe:
1. Consumer audit (identify all services hitting this GraphQL layer)
2. Migration strategy per consumer (direct API, new service, etc.)
3. Parallel-running period for traffic validation
4. Shutdown sequence and rollback plan]

## Alternatives considered

| Alternative | Why rejected |
|---|---|
| Rewrite service in TypeScript/Go | High effort; consumers can be migrated directly |
| Keep service, freeze features | Tech debt stays; still blocks /compact deprecation |

## Impact

| Area | Impact |
|---|---|
| UCV Regular/Lite | Must migrate off this layer before shutdown |
| /compact deprecation | Decommission unblocks hard /compact sunset |
| Performance | Expected improvement — fewer service hops |
| Monitoring | [TO COMPLETE — confirm existing alerting covers cutover] |

## Open questions

- Full consumer list: Owner: engineering. Target: [date].
- Parallel-run duration before shutdown: Owner: engineering lead. Target: [date].

## Decision

[TO COMPLETE — update when RFC is resolved]
