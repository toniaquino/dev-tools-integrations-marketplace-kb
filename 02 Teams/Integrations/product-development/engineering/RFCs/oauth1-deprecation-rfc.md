# STUB: Content to be completed — seeded 2026-06-19
# Source: Jira epic API-2463 (Backlog Q3 2026 as of 2026-06-19)
# Format: see .claude/writing-guides/rfc-guide.md

# RFC: Deprecate OAuth1 Token Usage -- Q3 2026

**Author:** [TO COMPLETE — engineering lead for API-2463]
**Status:** Backlog — not yet in review
**Jira epic:** API-2463
**Review by:** [TO COMPLETE — target Q3 2026]
**Reviewers:** Todd Willms, Todd Willms, [security/platform team]

---

## Summary

[TO COMPLETE — deprecate OAuth1-based authentication tokens in the Bynder API,
migrating all consumers to OAuth2, to improve security posture and reduce
authentication surface area]

## Motivation

[TO COMPLETE — describe OAuth1 weaknesses vs. OAuth2: signature complexity, lack of
token refresh, weaker security guarantees, and industry-standard direction toward
OAuth2/PKCE. Include any compliance or security audit drivers if applicable]

## Scope of impact

- **Partners affected:** [TO COMPLETE — all integration partners currently using OAuth1 tokens]
- **Internal consumers:** [TO COMPLETE — any internal services using OAuth1]
- **Traffic baseline:** [TO COMPLETE — current OAuth1 token usage]

## Proposal

[TO COMPLETE — describe:
1. Partner communication plan
2. OAuth2 migration guide for existing OAuth1 integrations
3. Deprecation notice period
4. Hard sunset date and enforcement mechanism]

## Alternatives considered

| Alternative | Why rejected |
|---|---|
| Keep OAuth1 indefinitely | Ongoing security risk; maintenance burden |
| Auto-upgrade OAuth1 sessions to OAuth2 | Not feasible — different token model |

## Impact

| Area | Impact |
|---|---|
| Security | Positive — removes weaker auth mechanism |
| Partners | Requires migration action |
| API surface | Breaking change for OAuth1 consumers — requires version management |
| Internal services | [TO COMPLETE — audit required] |

## Open questions

- Number of active OAuth1 integration partners: Owner: engineering/API team. Target: before RFC approval.
- Hard sunset date: Owner: Todd Willms. Target: Q3 2026 (to be confirmed).
- Is there a self-service migration tool or just documentation? Owner: TBD.

## Decision

[TO COMPLETE — update when RFC is resolved]
