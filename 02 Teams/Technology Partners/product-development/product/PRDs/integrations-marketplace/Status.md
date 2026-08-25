# Integrations Marketplace -- status

**Last updated:** 2026-08-25
**PM:** Bas van Reeuwijk
**Status:** 🟡

## This week

- **Certification Program:** Two new partner integrations entered the certification queue
  this week: Raspberry AI (MP-269, Awaiting Certification since 2026-08-19, parented under
  Release Q4.1 (2026)/MP-259, joining CloudCannon there) and Beautiful.ai (MP-251, Awaiting
  Certification since 2026-08-19, no parent epic assigned). Both assigned to Bas van
  Reeuwijk. The five Release Q3.2 (2026) items that moved to Awaiting Release last week
  (Vista Social/MP-264, Fluiid4-CLX/MP-260, Brandfolder Migration Tool-Gournay/MP-258,
  Fadel-Gournay Consulting/MP-257, Corsearch/MP-254) show no further Jira movement this
  week -- still Awaiting Release, not yet Released. *(Source: Jira board MP, direct issue
  lookup)*
- **Partner Onboarding / Doc Migration (ambiguous ownership, unresolved 2nd week
  running):** Confluence restructuring continues -- 71 more pages in the INTEGRATE space
  were touched by Bas van Reeuwijk between 2026-08-18 and 2026-08-25, continuing the
  single-table -> per-partner-page migration (built on the "Partner Integration Article
  TEMPLATE", page 6401753122) flagged last week. All 71 edits are individual partner pages
  (e.g. Salsify, Bynder Plugin for Figma, Shopify/Dataggo, several Akeneo connectors,
  Contentstack, Kentico Xperience, the CI-Hub connector family). None of the three
  canonical overview/blueprint pages (IAL blueprint, Certification Program overview,
  Partner Integrations & Connectors directory) were touched this week. Still no Jira epic
  or Slack thread disambiguates whether this is a Doc Migration wave, a Partner Onboarding
  process change, or both -- last week's ask to Bas for a decision has not been answered.
  *(Source: Confluence INTEGRATE space)*
- **Integration Abstraction Layer:** No signal from any source for an eighth consecutive
  cycle. The pilot-adapter milestone (target 2026-06-30) is now exactly 8 weeks overdue
  with nothing confirming completion or slippage. *(Source: absence of signal,
  cross-checked across Jira/Slack/Confluence)*
- **Slack:** Both channels scanned successfully (`ok: true` on both -- 10 messages in
  #b-team-integrations, 3 in #b-help-global-partnerships). All messages were
  partner-support/customer-escalation threads (an SNS webhook SignatureVersion permissions
  question, Twinings' unusable batch of 20 Adobe CC keys, a Figma-plugin account-tier
  question, an integration-request triage bot post, a forwarded UCV/PoD question, a Studio
  Gateway deprecation affecting a Figma OAuth callback, a Pixelz-integration access
  question for School Outfitters, a Jira-connector prospect need from the Läderach deal
  (~70K ARR), a HubSpot integration sell-motion question, and a new TTC lead requesting a
  custom Lucid Link integration) -- none relate to the four tracked features and no
  PM-level decisions were logged. No messages from Bas this week. *(Source: Slack
  #b-team-integrations, #b-help-global-partnerships)*
- **Feature launch completeness check:** No Jira epics moved to Done/Released in the last
  7 days, so there is nothing new to check against feature-index.yaml this cycle. *(Source:
  Jira board MP)*

## Blockers

- **Pencil.ai (MP-249)** stalled in Awaiting Certification for ~6 weeks (since
  2026-07-13), no movement this week either -- owner: Bas van Reeuwijk.
- **BrightCarbon (MP-266)** in Awaiting Certification since 2026-08-05 (~3 weeks), still no
  movement -- owner: Bas van Reeuwijk.
- **IAL pilot-adapter milestone** (target 2026-06-30) now 8 weeks overdue and
  unconfirmed -- owner: Bas van Reeuwijk.
- **Confluence restructuring ownership** (Doc Migration vs. Partner Onboarding) unresolved
  for a second consecutive week -- owner: Bas van Reeuwijk.

## Coming up

- Confirm with Bas whether the Confluence partner-directory restructuring is Doc
  Migration, Partner Onboarding, or both, and whether it needs a Jira epic -- carried over
  unresolved from last week.
- Track Raspberry AI (MP-269) and Beautiful.ai (MP-251) through the certification queue.
- Track the five Release Q3.2 (2026) items (Vista Social, Fluiid4, Brandfolder Migration
  Tool, Fadel, Corsearch) through to actual Release; follow up on the continued Pencil.ai
  and BrightCarbon stalls.

## Features

| Feature | Status | Last signal |
|---|---|---|
| Integration Abstraction Layer | 🟡 In progress / some risk | No signal for an 8th consecutive cycle; 2026-06-30 pilot-adapter target now exactly 8 weeks overdue, unconfirmed (absence of signal, cross-checked Jira/Slack/Confluence) |
| Certification Program | 🟡 In progress | 2026-08-19 (Jira board MP) -- Raspberry AI (MP-269) and Beautiful.ai (MP-251) entered Awaiting Certification; the 5-item Release Q3.2 (MP-253) wave remains Awaiting Release with no movement; Pencil.ai (MP-249) and BrightCarbon (MP-266) still stalled |
| Doc Migration | 🟡 In progress / unconfirmed | 2026-08-25 (Confluence, INTEGRATE space) -- 71 more pages restructured, continuing prior wave; still unconfirmed by Jira or Slack, ownership vs. Partner Onboarding unresolved for a 2nd week; last confirmed Jira wave remains 2026-07-13 (MP-242, Done) |
| Partner Onboarding | 🟡 In progress | 2026-08-25 (Confluence, INTEGRATE space) -- 71 more per-partner pages built/edited (2026-08-18 to 2026-08-25), continuing prior week's restructuring; overview/directory page itself not touched this week |
