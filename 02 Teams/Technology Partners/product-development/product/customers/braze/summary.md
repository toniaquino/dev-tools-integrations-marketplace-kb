# Braze — partner summary

> **Canonical entry:** `02 Teams/Connectors/Partner Integrations.md` → `## Braze`.
> This is a pointer stub, not a second source of truth. Status, ownership, integration history,
> contacts, open items and log all live there — add and update detail there, not here. That file
> is the repo's only structured partner-entry format and is read by Routine 8 in
> `content-variations-delivery-performance-kb` for the Confluence seed (see repo root
> `Governance.md` → "Confluence seed").

> **Filed here for consistency with the other partner stubs, but note that Braze is not a
> Technology Partners partner in the normal sense.** Ownership is shared: Meghan Dussault
> (Partnerships) owns the strategic partnership, Tony Smith (Connectors) owned the Bynder-built
> connector track, Bas van Reeuwijk owns Braze-side onboarding and any future marketplace intake.
> Toni Aquino arbitrated the split in June 2026. There is Connectors history here too, in the
> closed INC-1239 epic.

**Segment:** Strategic partner (Braze is also a paying Bynder customer, and Bynder appears to be a Braze customer)
**Relationship owner:** Shared — see above
**Tracked in:** No MP ticket, no INTEGRATE article, no Bynder Marketplace listing. Connectors history in [INC-1239](https://bynder.atlassian.net/browse/INC-1239) (closed, not pursued), [INC-1240](https://bynder.atlassian.net/browse/INC-1240), [INC-1315](https://bynder.atlassian.net/browse/INC-1315), and the still-open [INC-1335](https://bynder.atlassian.net/browse/INC-1335). Legal history in [BLT-2925](https://bynder.atlassian.net/browse/BLT-2925) (MNDA, 2023).

## Why this partner matters to this squad

Braze is the inverse of every other partner in this domain: **Bynder is the applicant, going
through Braze's onboarding programme**, with no Bynder-side agreement, no marketplace listing and
no built integration. That makes it the most useful case in the vault for two things:

- **Partner Onboarding Process** — Bynder is currently experiencing someone else's version of the
  process it is trying to improve, and Braze's is more instrumented: percentage-complete tracking,
  phased gates, automated next-step nudges, a self-serve Partner Fleet directory listing. Worth
  studying directly. It also produced a failure mode Bynder should recognise: Braze approved
  Bynder's application on 2026-02-25 and the notification never reached the owner, costing a month
  until Bas told their support he had never seen an agreement. **Bynder's own approval
  notifications are worth auditing for the same gap.**
- **Marketplace Documentation Migration / KB hygiene** — two defects here are systemic, not
  cosmetic. INC-1240 reads as documentation of a shipped integration (use cases, file-size limits,
  rate limits, a test environment with QA steps for webhooks) when nothing was ever built and the
  epic is closed; and the connectors weekly-synthesis routine reported the abandoned INC-1239 as
  "shipped to production" on both 2026-08-11 and 2026-08-14, needing a human correction each time.
  Toni Aquino's read was hardcoded automation rather than the closure status. **A
  closed-as-abandoned epic surfacing as a shipped feature will recur until that is fixed.**

Two things to watch. First, **a listing is about to publish with nothing behind it**: Braze
accepted Bynder's documentation on 2026-08-18 and said Bynder should launch soon, describing the
UCV Chrome extension. Toni Aquino's standing constraint is not to position a copy/paste workflow
as an integrated solution, and nobody has written down how Bynder squares those two externally —
nor is there any Bynder-side article for support and sales to point at. Second, **the commercial
channel just opened for the first time in three years**: Braze introduced a US contact for account
mapping and joint sales opportunities on 2026-08-17, and no one has been assigned to run it.

Useful negative finding worth preserving: the Braze Catalogs personalisation use case Bynder built
its i-Hub plan around **has no demand behind it** — customer conversations in June 2026 found the
lead account does not use Catalogs at all, and none use them the way Bynder assumed. That, plus
three separate findings across 2023, February 2026 and May 2026 that the Braze API cannot support a
Bynder-built connector, is why the build was dropped twice.

## Sources

- Jira: [INC-1239](https://bynder.atlassian.net/browse/INC-1239), [INC-1240](https://bynder.atlassian.net/browse/INC-1240), [INC-1315](https://bynder.atlassian.net/browse/INC-1315), [INC-1335](https://bynder.atlassian.net/browse/INC-1335) (open, unassigned), [BLT-2925](https://bynder.atlassian.net/browse/BLT-2925), [BLT-5952](https://bynder.atlassian.net/browse/BLT-5952), [ISEC-17271](https://bynder.atlassian.net/browse/ISEC-17271), plus PS4 customer tickets. Also a Productboard note, "Braze native integration to Bynder".
- Slack: `#external-bynder-braze` (shared channel), `#b-team-integrations`, `#b-help-global-partnerships`, `#b-help-integrationshub`, and group DMs covering the June 2026 ownership discussion and the August 2026 synthesis corrections.
- Gmail label `Marketplace Partners/Braze` — 57 threads / 77 messages, 2023-08-16 → 2026-08-18. **The large majority is Braze's own partner-programme and marketing mail**; roughly a dozen threads are substantive. Slack carries more of this relationship than email does.
- Bynder-authored Google Docs (no Confluence equivalent exists): a three-approaches overview including the shared client list, the Braze API feedback document, and the Braze listing submission draft.
