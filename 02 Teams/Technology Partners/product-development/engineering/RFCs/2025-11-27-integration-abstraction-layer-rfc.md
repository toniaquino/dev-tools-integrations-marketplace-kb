# RFC: Integration Abstraction Layer (IAL) — 2025-11-27

**Author:** Bas van Reeuwijk
**Status:** In progress
**Jira epic:** [TO COMPLETE — no Jira board configured]
**Review by:** [TO COMPLETE]
**Reviewers:** [TO COMPLETE — engineering lead, backend, platform engineer]
**Confluence source:** https://bynder.atlassian.net/wiki/spaces/INTEGRATE/pages/5675221021
**Last updated in Confluence:** 2025-11-27

---

## Summary

Establish a unified, resilient, and observable Integration Abstraction Layer (IAL) that standardises how Bynder integrates with external systems. Provides consistent contracts, reduces coupling, accelerates partner onboarding, and enforces security and governance across all integrations.

## Motivation

Each integration is currently built differently, with no standardised approach to auth, retries, observability, or error handling. This creates:
- High partner onboarding cost (manual, custom per integration)
- Inconsistent reliability and observability across the integration fleet
- Security and compliance risks from inconsistent auth/secret handling
- Engineering rework when provider APIs change

The IAL abstracts this complexity behind stable, versioned domain ports.

## Proposal

Domain-driven ports and adapters architecture (hexagonal) for all integrations.

### Logical components

- **Domain Ports** — Versioned interfaces aligned to business capabilities (e.g. Payments, Identity, Catalog). Defined as OpenAPI/Protobuf/AsyncAPI contracts.
- **Adapters/Connectors** — Provider-specific implementations mapped to common schemas. Each adapter maps the provider surface to the port contract.
- **Policy Layer** — AuthN/Z, rate limiting, quotas, schema validation, request shaping. Applied as middleware.
- **Resilience** — Retries with jitter, circuit breakers, bulkheads, timeout budgets, idempotency keys.
- **Observability** — Structured logs, metrics, traces with correlation IDs, audit trail.
- **Adapter SDK** — Common utilities for auth, retries, tracing, error taxonomy, test harness. Distributed to engineering teams (and potentially partners).
- **Message Bus** — Topics/queues for async commands/events; dead-letter strategy.

### API and schema standards

- Synchronous: REST with OpenAPI contracts or gRPC with Protobuf; consistent error model
- Asynchronous: AsyncAPI specs; envelopes with correlationId, causationId, tenantId
- Versioning: Semantic versioning for ports; backward-compatible changes preferred

### Security

- Authentication: OIDC client credentials, Mutual TLS, or signed payloads per adapter
- Authorization: Least privilege, scoped tokens, per-port RBAC, attribute-based policies
- Data protection: Field-level encryption, tokenization, deterministic hashing for PII
- Compliance: DPIA, records of processing, retention policies, regional data residency
- Never pass secrets via logs or traces. Enforce secret scanning and redaction at ingress and egress.

### Error taxonomy

```json
{
  "errorCategory": "UpstreamFailure|Validation|Auth|RateLimit|Timeout|Conflict|Unknown",
  "retryable": true,
  "httpStatus": 502,
  "providerCode": "E1234",
  "message": "Upstream service temporarily unavailable",
  "correlationId": "{uuid}"
}
```

## Alternatives considered

| Alternative | Why rejected |
|---|---|
| Continue building integrations ad-hoc | Does not scale; no consistency in reliability, observability, or auth. Partner onboarding stays slow. |
| Build a custom UI for partner management | Out of scope for IAL — API-first approach preferred. Admin console handles management layer. |
| Long-term ETL/analytics pipelines in IAL | Handed off to data platform — outside IAL scope. |

## Impact

| Area | Impact |
|---|---|
| Performance | P50 <100ms sync, P95 <300ms; async SLAs documented per topic |
| Scalability | Horizontal scaling with backpressure and concurrency controls |
| Security | Centralised auth, secret scanning, DPIA compliance |
| Existing APIs | Non-breaking where possible; deprecation window with dual-running adapters |
| Other teams | Engineering: SDK reduces per-adapter rework. Partnership: faster onboarding. CS: better observability for issue diagnosis. |

## Milestones

| Milestone | Target date | Status |
|---|---|---|
| Architecture and ADRs complete | 2026-03-31 | In progress |
| First port contract (Payments v1) published | 2026-05-15 | In review |
| Pilot adapter live with feature flags | 2026-06-30 | On track |
| Adapter SDK available | 2026-05-01 | [TO COMPLETE] |
| Reference adapter and sample client SDK | 2026-06-10 | [TO COMPLETE] |

## Non-functional requirements

- Availability: Core ports >= 99.9%; graceful degradation for non-critical paths
- Latency: P50 < 100ms sync, P95 < 300ms; async SLAs per topic
- MTTR: < 15 minutes with automated rollback

## Open questions

- Who is the tech lead responsible for the Adapter SDK implementation? Owner: Bas. Target: [TO COMPLETE]
- Will the Adapter SDK be distributed externally to technology partners? Owner: Bas. Target: [TO COMPLETE]
- Which integration is the pilot adapter? Owner: [TO COMPLETE]. Target: 2026-06-30.

## Decision

[TO COMPLETE — update when architecture decisions are finalised and ADRs are approved]

## Operational readiness

- Runbooks: Incident playbooks, health checks, rollback and manual failover steps
- Dashboards: Error rates, saturation, latency, retries, circuit breaker states
- Alerting: SLO-based alerts with burn-rate policies
