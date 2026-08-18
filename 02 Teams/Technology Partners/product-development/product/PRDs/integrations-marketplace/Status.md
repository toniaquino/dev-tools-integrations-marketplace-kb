# Integrations Marketplace -- status

**Last updated:** 2026-08-18
**PM:** Bas van Reeuwijk
**Status:** 🟡

## This week

- **Certification Program:** Five partner integrations advanced from Awaiting Certification
  to Awaiting Release on 2026-08-14, all parented under the Release Q3.2 (2026) epic
  (MP-253, itself still Backlog): Vista Social (MP-264), Fluiid4/CLX (MP-260), Brandfolder
  Migration Tool/Gournay (MP-258), Fadel/Gournay Consulting (MP-257), and Corsearch
  (MP-254). The Vista Social transition is directly confirmed against last week's
  2026-08-05 snapshot (was Awaiting Certification) and corroborated by its new Confluence
  partner page, which explicitly states "Jira MP-264 is in Awaiting Release." One new item
  entered the certification queue: CloudCannon (MP-267, Awaiting Certification since
  2026-08-13, parented under Release Q4.1 (2026)/MP-259). Pencil.ai (MP-249) remains
  stalled in Awaiting Certification, touched again 2026-08-12 with no status change -- now
  ~5 weeks (since 2026-07-13). BrightCarbon (MP-266) unchanged since 2026-08-05 (Awaiting
  Certification, ~13 days). MP-82 epic still Backlog, unchanged since 2025-10-07. *(Source:
  Jira board MP, direct issue lookup; cross-referenced with Confluence partner pages)*
- **Partner Onboarding:** Major documentation restructuring in Confluence -- the "Partner
  Integrations & Connectors" overview page (1920630816) was converted from one large
  inline status table (v302, ~372KB) to a page-tree of individual partner pages via a
  Confluence "children" macro (v307, 2026-08-17). Roughly 246 pages across the INTEGRATE
  space were touched by Bas van Reeuwijk between 2026-08-11 and 2026-08-18, built from a
  new "Partner Integration Article TEMPLATE" (page 6401753122, v6). The new per-partner
  pages line up with this week's certification/release movement -- dedicated pages now
  exist for Vista Social, Fluiid4 (CLX), Brandfolder Migration Tool (Gournay), Fadel
  (Gournay Consulting), Corsearch, and CloudCannon. No new connectors were reported
  released via the old-style tracker this week -- this reads as a structural/process
  change, not a new-release signal. No Jira epic or Slack thread confirms this as an
  official initiative. *(Source: Confluence INTEGRATE space)*
- **Doc Migration:** No new Jira signal -- Release Q3.1 (2026) (MP-242, Done 2026-07-13)
  remains the last confirmed wave. The Confluence restructuring described above under
  Partner Onboarding could plausibly represent the next Doc Migration wave (it is, after
  all, a migration of partner documentation into a new structure), but it is filed under
  Partner Onboarding here because that is the feature whose canonical Confluence page
  (1920630816) was directly restructured; no Jira epic or Slack thread disambiguates which
  initiative owns this work. **Flagging for Bas to confirm which initiative this belongs
  to, and whether it needs a Jira epic.** *(Source: Jira board MP -- absence of signal;
  Confluence -- unconfirmed, ambiguous ownership)*
- **Integration Abstraction Layer:** No signal from any source for a seventh consecutive
  cycle. The pilot-adapter milestone (target 2026-06-30) is now 7 weeks overdue with
  nothing confirming completion or slippage -- still a flagged risk, not a confirmed miss.
  *(Source: absence of signal, cross-checked across Jira/Slack/Confluence)*
- **Slack:** Both channels scanned successfully (`ok: true` on both). All messages in both
  channels were partner-support/customer-escalation threads (Canva domain-error tickets
  affecting 4 customers, Optimizely connector 8.6.0 release note with 9.0 preview, Figma
  preset/metadata question, Contentful sync-delay request referencing Gournay's connector,
  Adobe CC/LinkrUI self-signed-certificate issue, AWS co-sell process question, Marketo
  multi-sub-brand question, and several others) -- no PM-level decisions logged for the
  four tracked features. *(Source: Slack #b-team-integrations, #b-help-global-partnerships)*
- **Feature launch completeness check:** No Jira epics moved to Done/Released in the last
  7 days, so there is nothing new to check against feature-index.yaml this cycle. *(Source:
  Jira board MP)*

## Blockers

- **Pencil.ai (MP-249)** stalled in Awaiting Certification for ~5 weeks (since
  2026-07-13) -- owner: Bas van Reeuwijk.
- **IAL pilot-adapter milestone** (target 2026-06-30) now 7 weeks overdue and
  unconfirmed -- owner: Bas van Reeuwijk.
- **BrightCarbon (MP-266)** in Awaiting Certification since 2026-08-05 (~13 days), no
  movement this week -- owner: Bas van Reeuwijk.

## Coming up

- Confirm with Bas whether the Confluence partner-directory restructuring (single table ->
  per-partner pages) is an intentional Doc Migration wave, an onboarding-process change,
  or both -- and whether it needs a Jira epic to track it going forward.
- Track the five Release Q3.2 (2026) items now Awaiting Release (Vista Social, Fluiid4,
  Brandfolder Migration Tool, Fadel, Corsearch) through to actual release.
- Track CloudCannon (MP-267) through the certification queue; follow up on Pencil.ai's
  continued stall and BrightCarbon's lack of movement.

## Features

| Feature | Status | Last signal |
|---|---|---|
| Integration Abstraction Layer | 🟡 In progress / some risk | No signal for a 7th consecutive cycle; 2026-06-30 pilot-adapter target now 7 weeks overdue, unconfirmed (absence of signal, cross-checked Jira/Slack/Confluence) |
| Certification Program | 🟡 In progress | 2026-08-14 (Jira board MP) -- 5 items (MP-264, MP-260, MP-258, MP-257, MP-254) moved Awaiting Certification -> Awaiting Release under Release Q3.2 (MP-253); CloudCannon (MP-267) entered queue 2026-08-13; Pencil.ai (MP-249) still stalled since 2026-07-13 |
| Doc Migration | 🟡 In progress / unconfirmed | 2026-08-17 (Confluence, page 1920630816 v307) -- possible next-wave restructuring, unconfirmed by Jira or Slack, ambiguous ownership vs. Partner Onboarding; last confirmed Jira wave remains 2026-07-13 (MP-242, Done) |
| Partner Onboarding | 🟡 In progress | 2026-08-17 (Confluence, INTEGRATE space, page 1920630816 v307) -- partner directory restructured into ~246 per-partner template pages; new pages line up with partners currently moving through certification/release |
