# Integrations Marketplace -- status

**Last updated:** 2026-09-01
**PM:** Bas van Reeuwijk
**Status:** 🟢

## This week

- **Certification Program:** All five Release Q3.2 (2026) items that were "Awaiting
  Release" as of last week's synthesis (2026-08-14) have now shipped -- moved to
  RELEASED in Jira: Corsearch (MP-254, released 2026-08-28), Brandfolder Migration
  Tool/Gournay (MP-258, released 2026-08-27), Fadel/Gournay Consulting (MP-257, released
  2026-08-27), Fluiid4/CLX (MP-260, released 2026-08-31), and Vista Social (MP-264,
  released 2026-08-31). All still parented under Release Q3.2 (2026) (MP-253, itself
  still Backlog). Two new items entered active development under Release Q4.1 (2026)
  (MP-259): Dyspatch (MP-270, Under Development as of 2026-08-27) and Bynder DAM
  Connector for Umbraco/Uxbee (MP-271, Under Development as of 2026-08-31). Pencil.ai
  (MP-249), BrightCarbon (MP-266), and CloudCannon (MP-267) had no Jira activity this
  week -- no change to their queue positions. *(Source: Jira board MP, direct issue
  lookup)*
- **Certification Program (Confluence corroboration):** Dedicated Confluence pages for
  all five newly-released partners (Vista Social, FLUiiD4 (CLX Europe), Corsearch/Image
  Rights Compliance, FADEL, Brandfolder Migration Tool) plus the two new Q4.1
  development items (Dyspatch, Bynder DAM Connector for Umbraco) were touched this
  week, consistent with the per-partner template structure established 2026-08-17 --
  no new restructuring event, just routine status updates on existing per-partner
  pages. *(Source: Confluence INTEGRATE space)*
- **Certification Program (new pipeline signal, Slack):** Bas confirmed in
  #b-team-integrations (2026-08-26) that the Raspberry AI integration "has been
  validated" and "is scheduled for release on our marketplace in the 2026 Q4.1 cycle" --
  in response to a partner (Garan Inc., ~$180k ARR opportunity) asking about Raspberry
  AI x Bynder connectivity. This integration does not yet appear in this week's Jira
  MP-board activity, so it has no epic/issue key yet in feature-index.yaml. *(Source:
  Slack #b-team-integrations -- decision from Bas, no Jira issue yet)*
- **Doc Migration / Partner Onboarding:** No new Jira, Slack, or Confluence signal this
  week beyond the routine per-partner page touches noted above. The ownership question
  flagged last week (2026-08-17 restructuring -- is it Doc Migration, Partner
  Onboarding, or both?) remains unconfirmed by Bas. **Still flagging for PM
  confirmation.** *(Source: absence of signal, cross-checked Jira/Slack/Confluence)*
- **Integration Abstraction Layer:** No signal from any source for an 8th consecutive
  cycle. The pilot-adapter milestone (target 2026-06-30) is now approximately 9 weeks
  overdue with nothing confirming completion or slippage -- still a flagged risk, not a
  confirmed miss. The canonical Confluence blueprint page (5675221021) is unchanged
  since 2025-11-27. *(Source: absence of signal, cross-checked across Jira/Slack/Confluence)*
- **Slack (general scan):** Both channels scanned successfully (`ok: true` on both).
  Beyond the Raspberry AI decision above, all other messages in both channels were
  partner-support/customer-escalation threads (Contentstack migration question for Park
  Holidays, Contentful upload-limitation escalation from Scentre Group, Sanity light-user
  question, Workfront project-vs-task-level asset question from Guidewell, a webhook
  investigation for Patient Point, a Rabobank CDN-invalidation/webhook question, a Getty
  sync-delay report, Seismic pricing question, a Nine United PIM full-sync rollback
  question, Box tagging question, a Wella Mulesoft/SAP metadata issue, a SailPoint/Folloze
  integration request, a Sitecore XM/XP-vs-AI contract question for Emory, a Drupal
  multi-instance question, and partner-referral leads for Global Partners, Mass General
  Brigham, and Cotopaxi in #b-help-global-partnerships) -- no other PM-level decisions
  logged for the four tracked features. *(Source: Slack #b-team-integrations,
  #b-help-global-partnerships)*
- **Feature launch completeness check:** No Jira **epics** (issuetype = Epic) moved to
  Done/Released in the last 7 days -- the five items that shipped this week are
  child "Technology Partner Integration" issues under the still-Backlog Release Q3.2
  (2026) epic (MP-253), not epics themselves, so there is nothing new to check against
  feature-index.yaml under this check's Epic-level scope this cycle. *(Source: Jira
  board MP)*

## Blockers

- **Pencil.ai (MP-249)** stalled in Awaiting Certification for ~7 weeks (since
  2026-07-13), no Jira activity this week -- owner: Bas van Reeuwijk.
- **IAL pilot-adapter milestone** (target 2026-06-30) now ~9 weeks overdue and
  unconfirmed -- owner: Bas van Reeuwijk.
- **BrightCarbon (MP-266)** in Awaiting Certification since 2026-08-05 (~4 weeks), no
  movement this week -- owner: Bas van Reeuwijk.
- **Doc Migration vs. Partner Onboarding ownership** of the 2026-08-17 Confluence
  restructuring remains unconfirmed by Bas, now over 2 weeks outstanding -- owner: Bas
  van Reeuwijk.

## Coming up

- Track Dyspatch (MP-270) and Bynder DAM Connector for Umbraco/Uxbee (MP-271) as they
  move from Under Development into the certification queue under Release Q4.1 (2026).
- Confirm with Bas whether Raspberry AI has (or needs) a Jira epic/issue to track its
  path into the Q4.1 release cycle.
- Continue to follow up on Pencil.ai's and BrightCarbon's stalled certification queue
  positions, and CloudCannon's progress through certification.
- Still need Bas to confirm ownership of the 2026-08-17 Confluence restructuring (Doc
  Migration vs. Partner Onboarding vs. both).

## Features

| Feature | Status | Last signal |
|---|---|---|
| Integration Abstraction Layer | 🟡 In progress / some risk | No signal for an 8th consecutive cycle; 2026-06-30 pilot-adapter target now ~9 weeks overdue, unconfirmed (absence of signal, cross-checked Jira/Slack/Confluence) |
| Certification Program | 🟢 On track | 2026-08-27 to 2026-08-31 (Jira board MP) -- 5 items (MP-254, MP-258, MP-257, MP-260, MP-264) released; 2 new items (MP-270, MP-271) entered development under Release Q4.1 (MP-259); Raspberry AI validated per Bas (Slack, 2026-08-26), targeting Q4.1, no Jira issue yet |
| Doc Migration | 🟡 In progress / unconfirmed | No new signal this week; last confirmed Jira wave remains 2026-07-13 (MP-242, Done); ownership of 2026-08-17 Confluence restructuring vs. Partner Onboarding still unconfirmed |
| Partner Onboarding | 🟡 In progress | No new restructuring this week; per-partner pages for newly released/in-development items (Vista Social, FLUiiD4, Corsearch, Brandfolder, Fadel, Dyspatch, Uxbee) updated on the template established 2026-08-17 |
