# Integrations Marketplace -- status

**Last updated:** 2026-08-04
**PM:** Bas van Reeuwijk
**Status:** 🟡

## This week

- **Partner Onboarding:** Real movement this week. The Confluence "Partner Integrations
  & Connectors" page (linked feature page) was edited 2026-08-03 by Bas van Reeuwijk --
  five partner connectors moved from IN REVIEW to RELEASED: Asset Uploader (Gournay
  Consulting), ButterCMS, Drupal (MDSystems), Inriver (Ntara), and Salsify (Lettuce). A
  new partner connector was also added to the tracker: Brandfolder Migration Tool
  (Gournay Consulting), status IN REVIEW, targeting August 2026. *(Source: Confluence
  INTEGRATE space, page 1920630816, diffed v300 -> v301)*
- **Certification Program:** No new Jira activity this week (0 MP issues updated in the
  7-day window). Direct issue lookups confirm MP-264 (Vista Social) unchanged since
  2026-07-24 (Awaiting Certification) and MP-82 epic unchanged since 2025-10-07
  (Backlog). *(Source: Jira board MP)*
- **Certification Program (correction):** Pencil.ai (MP-249) was recorded last cycle as
  stalled "since 2026-07-01 (4 weeks)." A direct Jira lookup this cycle shows the
  issue's actual `updated` timestamp is 2026-07-13, not 2026-07-01 -- so it is stalled
  in Awaiting Certification for ~3 weeks, not 4. Prior cycle appears to have used the
  issue's created date. Corrected in feature-index.yaml this cycle. *(Source: Jira
  board MP, direct issue lookup)*
- **Doc Migration:** No new activity this week. Release Q3.1 (2026) (MP-242, Done
  2026-07-13) remains the last confirmed wave; next wave epic still not identified.
  *(Source: Jira board MP -- absence of new signal)*
- **Integration Abstraction Layer:** No signal from any source for a fifth consecutive
  cycle. The pilot-adapter milestone (target 2026-06-30) is now 5 weeks overdue with
  nothing confirming completion or slippage -- still a flagged risk, not a confirmed
  miss. *(Source: absence of signal, cross-checked across Jira/Slack/Confluence)*
- **Slack:** Both channels scanned successfully this week, including
  #b-help-global-partnerships, which was unreadable for the prior two cycles (flagged
  2026-07-20 and 2026-07-28) -- that data-source gap appears resolved. All messages in
  both channels were partner-support/customer-escalation threads (Monday.com asset-size
  limits, SFCC staging-environment question, Getty partial-upload question, Drupal
  media-field and asset-title-length bugs, LinkrUI license-visibility question,
  Syndigo/Salsify automation questions, Workfront zip-file question, Veriflies pricing
  question, Kentico integration-ownership question, partner-lead referrals) -- no
  PM-level decisions logged for the four tracked features. *(Source: Slack
  #b-team-integrations, #b-help-global-partnerships)*

## Blockers

- **IAL pilot-adapter milestone** (target 2026-06-30) now 5 weeks overdue and
  unconfirmed -- owner: Bas van Reeuwijk.
- **Pencil.ai (MP-249)** stalled in Awaiting Certification for ~3 weeks (since
  2026-07-13, corrected from prior cycle's ~4-week figure) -- owner: Bas van Reeuwijk.

## Coming up

- Track the 5 newly RELEASED partner connectors through to certification-queue
  follow-through, if applicable.
- Watch Brandfolder Migration Tool (Gournay Consulting) -- newly added to the partner
  tracker (IN REVIEW, targeting August 2026); also tracked separately in Jira under
  MP-258 for certification.
- Bas to confirm actual status of the IAL pilot adapter now that the 2026-06-30 target
  is 5 weeks overdue without a recorded update.
- Pencil.ai (MP-249) has been stalled in Awaiting Certification for ~3 weeks -- may need
  PM follow-up with the partner or a process check.
- Track Vista Social (MP-264) through certification -- no movement since it opened
  2026-07-24.

## Features

| Feature | Status | Last signal |
|---|---|---|
| Integration Abstraction Layer | 🟡 In progress / some risk | No fresher signal since 2026-06-19; Confluence blueprint page unedited since 2025-11-27; 2026-06-30 pilot-adapter target now 5 weeks overdue, unconfirmed |
| Certification Program | 🟡 In progress / some risk | 2026-08-04 (Jira board MP, direct lookup) -- MP-264 (Vista Social) unchanged since 2026-07-24, Awaiting Certification; MP-249 (Pencil.ai) unchanged since 2026-07-13 (~3 weeks, corrected this cycle) |
| Doc Migration | 🟢 On track | 2026-07-13 (Jira board MP) -- Release Q3.1 (2026) epic (MP-242) moved to Done, closing the 5-partner doc migration wave; no new wave epic identified yet |
| Partner Onboarding | 🟢 Active | 2026-08-03 (Confluence, Partner Integrations & Connectors page) -- 5 connectors released, 1 new partner (Brandfolder Migration Tool) added |
