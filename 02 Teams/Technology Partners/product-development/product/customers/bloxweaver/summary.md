# BloxWeaver — partner summary

> **Canonical entry:** `02 Teams/Connectors/Partner Integrations.md` → `## BloxWeaver`.
> This is a pointer stub, not a second source of truth. Status, integration scope, contacts,
> open items and log all live there — add and update detail there, not here. That file is the
> repo's only structured partner-entry format and is read by Routine 8 in
> `content-variations-delivery-performance-kb` for the Confluence seed (see repo root
> `Governance.md` → "Confluence seed").

**Segment:** Technology partner (not a Bynder customer account)
**Relationship owner:** Bas van Reeuwijk (PM, Technology Partners & Marketplace)
**Tracked in:** **Nothing.** No Jira ticket, no INTEGRATE article, no Bynder Marketplace listing, no BLT legal ticket. The only Bynder-side records are the Gmail thread (label `Marketplace Partners/Bloxweaver`), the shared Slack channel `#external-bynder-bloxweaver`, and the executed Technology Partnership Agreement (v260325, 2026-07-21).

## Why this partner matters to this squad

BloxWeaver is the **best-case reference** for the Partner Onboarding Process workstream named in
`../../feature-index.yaml`, and the clearest illustration of where the process still fails.

**What went right — the numbers to beat.** Inbound HubSpot partner lead at 09:02 on 2026-07-20,
picked up 15 minutes later. Intro call the next day. Agreement sent 15:34, partner agreed to sign
at 15:51, Docusign complete at 19:33 — **same day, under four hours, no redlines, no legal ticket**.
Sandbox, Crossbeam and shared Slack all delivered 2026-07-22, with the partner connected and
testing that evening. Partner reported a working integration on 2026-07-23.

- **Lead → signed agreement: ~30 hours**
- **Lead → partner testing in a live sandbox: ~2.5 days**
- **Lead → partner reports working integration: 3 days**

Against CloudCannon (8 days to sign), Raspberry.ai (9 weeks) and Corsearch (11 months). Two
partners now show that when the template does not go to the partner's own counsel, Bynder-side
contracting is effectively instant — every slow case in this file was delayed by the partner's
legal team or Bynder's own legal backlog, not by the instrument.

**A finding worth carrying into the baseline:** the BloxWeaver Pipes connector was **already built
before first contact**, from Bynder's *public* API specification, with no sandbox. For a competent
partner, good public API docs take the sandbox off the critical path entirely — which reframes what
the onboarding process is actually for.

**What went wrong — and it is the whole point of this stub.** A signed partner with a working,
partner-built integration has **no Bynder-side tracking whatsoever**. Contrast Raspberry.ai and
CloudCannon, where a Jira ticket and an INTEGRATE article exist despite less working software.
BloxWeaver is invisible to the certification pipeline, to the weekly synthesis, and to anyone in
sales or support who asks whether Bynder integrates with it. No technical validation is booked, the
partner's two intro-call deliverables (demo, listing background) are outstanding, and **there has
been no contact since 2026-07-28** — three weeks after the strongest first week in this file.

Two API items also need escalating out of Slack: the missing **metaproperty / metaproperty-option
translations API** (confirmed roadmap, not public — BloxWeaver will adopt it when it ships), and a
separate defect where the taxonomy API **accepted `translations` fields and locale headers and
returned success without applying or exposing them**. Silent acceptance of unknown fields will
cause other partners to ship code they believe works. Neither has a ticket.

## Sources

- Gmail label `Marketplace Partners/Bloxweaver` — 4 threads / 11 messages, 2026-07-20 → 2026-07-22, summarised into the canonical entry's Log.
- Slack: `#external-bynder-bloxweaver` (created 2026-07-22) — **carries the technical substance of this relationship**, including the API gap exchange of 2026-07-23 → 2026-07-28. Also a DM of 2026-08-13 listing BloxWeaver among nine recently signed technology partners ([thread](https://bynder.slack.com/archives/D050VL3QL3S/p1786637349339599)).
- Zoom AI recap of the 2026-07-21 intro call — the only record of the partner profile and the programme walkthrough. Treat wording as approximate: it renders BloxWeaver as "Blocksweaver"/"BlockSaver" and Bynder as "Binder", and is internally inconsistent about whose API specification the connector was built from (Bynder's is correct).
- Docusign: "Bynder Technology Partnership Agreement v260325", all signers complete 2026-07-21.
- Jira: none. Confluence: none.
