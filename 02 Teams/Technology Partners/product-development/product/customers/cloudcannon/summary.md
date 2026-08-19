# CloudCannon — partner summary

> **Canonical entry:** `02 Teams/Connectors/Partner Integrations.md` → `## CloudCannon`.
> This is a pointer stub, not a second source of truth. Status, category, integration scope,
> marketplace-listing timing, contacts, open items and log all live there — add and update
> detail there, not here. That file is the repo's only structured partner-entry format and is
> read by Routine 8 in `content-variations-delivery-performance-kb` for the Confluence seed
> (see repo root `Governance.md` → "Confluence seed").

**Segment:** Technology partner (not a Bynder customer account)
**Relationship owner:** Bas van Reeuwijk (PM, Technology Partners & Marketplace)
**Tracked in:** [MP-267](https://bynder.atlassian.net/browse/MP-267) (board MP, Awaiting Certification, Release Q4.1 (2026) wave) and INTEGRATE article ["CloudCannon"](https://bynder.atlassian.net/wiki/spaces/INTEGRATE/pages/6508838916/CloudCannon)

## Why this partner matters to this squad

CloudCannon is the fast case, and it is more useful than the slow ones for the two
Integrations Marketplace workstreams this squad owns (both named in `../../feature-index.yaml`):

- **Partner Onboarding Process** — contracting took eight days end to end (agreement sent
  2026-06-24, fully executed 2026-07-02) through the self-serve `dam.bynder.com/by/tpa` route
  with no redlines and no Bynder Legal ticket, and the partner had a working prototype one day
  after the sandbox was provisioned. Against Raspberry.ai's nine-week legal stretch, this is
  the fast-path baseline. What did *not* go fast is everything after: Technical Validation was
  not booked until 2026-08-11 and is scheduled for 2026-08-25, six weeks after the working
  example, and after MP-267 was already raised. **The bottleneck in this partner's path is
  Bynder-side sequencing, not contracting or partner engineering** — a sharper finding than the
  Raspberry.ai case gives, because nothing else here was slow.
- **Marketplace Documentation Migration** — the INTEGRATE article was created 2026-08-13 from
  Bynder-side desk research rather than a partner intake form, so nearly every operational field
  is `TBC`. It also carries the same two wrong Slack channel names as the Raspberry.ai article
  (`#b-help-integrations`, `#b-help-partnerships`), which points at the template rather than
  either author.

Two things to watch. First, **an open sequencing question**: MP-267 is in Awaiting Certification
while Technical Validation is not until 2026-08-25 and every operational field is still `TBC`,
and that Jira state is already propagating into the weekly Technology Partners synthesis
(2026-08-14, 2026-08-19). Note this is *not* a Jira ↔ Confluence conflict — the INTEGRATE
article's State field is a simplified customer-safe view in which IN DEVELOPMENT covers every
Jira state before Released, so it cannot be used to read progress. Second, the **expired
customer deadline**: CloudCannon committed on 2026-06-24 to an eight-week implementation for
the joint account that drove the partnership, which lands ~2026-08-19, and nothing on the
Bynder side records whether it shipped.

## Sources

- Jira: [MP-267](https://bynder.atlassian.net/browse/MP-267) (created 2026-08-13, parent epic MP-259 "Release Q4.1 (2026)")
- Confluence: [CloudCannon](https://bynder.atlassian.net/wiki/spaces/INTEGRATE/pages/6508838916/CloudCannon) (INTEGRATE, created 2026-08-13)
- Slack: DM, 2026-08-13 — listed among nine technology partners signed in the preceding month ([thread](https://bynder.slack.com/archives/D050VL3QL3S/p1786637349339599)); Technology Partners weekly synthesis, 2026-08-14 and 2026-08-19 — certification-queue entry
- Gmail label `Marketplace Partners/CloudCannon` — 5 threads / 8 messages, 2026-05-28 → 2026-08-11, summarised into the canonical entry's Log. Main thread: "Bynder Technology Partnership"; the Technical Validation calendar notifications sit in Trash, outside the label.
