# Integrations Marketplace -- status

**Last updated:** 2026-09-15
**PM:** Bas van Reeuwijk
**Status:** 🟡

## This week

- **Reconciliation note:** the last synthesis merged to `main` was dated 2026-08-18.
  Routine A2's cron for this squad was paused 2026-08-20 (PR #7,
  "Pause Routine A2 (tech partners + integrations reply processing) schedule"), so the
  three weekly syntheses that ran since (2026-08-25, 2026-09-01, 2026-09-08) were pushed
  as branches but never opened/merged as PRs -- PR #12
  (`weekly-sync/techpartners-synthesis-2026-08-25`) is still open and unmerged; the 09-01
  and 09-08 branches have no PR at all. This update reconciles their accumulated findings,
  re-verified live against Jira today (2026-09-15), into the picture below rather than
  building only on the stale 2026-08-18 baseline. One item -- CloudCannon (MP-267) --
  dropped out of the "This week" narrative in all three unmerged cycles despite staying
  stalled the whole time; it's restored below. *(Source: repo branch/PR history, GitHub
  API; Jira board MP, direct issue verification)*
- **Certification Program -- shipped since last merged update:** the five Release Q3.2
  (2026) items that were "Awaiting Release" as of 2026-08-14 all moved to RELEASED between
  2026-08-27 and 2026-08-31: Corsearch (MP-254, 2026-08-28), Brandfolder Migration
  Tool/Gournay (MP-258, 2026-08-27), Fadel/Gournay Consulting (MP-257, 2026-08-27),
  Fluiid4/CLX (MP-260, 2026-08-31), Vista Social (MP-264, 2026-08-31). *(Source: Jira
  board MP, direct issue verification 2026-09-15)*
- **Certification Program -- new queue entries:** six further items entered Awaiting
  Certification since: Raspberry AI (MP-269, 2026-09-02), Bynder DAM Connector for
  Umbraco/Uxbee (MP-271, 2026-09-02), Tiled (MP-272, 2026-09-02), Veeva Vault/Klick
  (MP-261, 2026-09-03, parented under Release Q3.2 (2026)/MP-253), Bynder Bridge --
  WordPress/Seventyone Studio (MP-273, 2026-09-03), and Dyspatch (MP-270, 2026-09-04) --
  the latter four plus Raspberry AI and the Umbraco connector parented under Release Q4.1
  (2026)/MP-259. No epics moved to Done/Released. Release Q3.2 (MP-253), Release Q4.1
  (MP-259), and the Certification Program epic (MP-82) all remain Backlog. *(Source: Jira
  board MP, direct issue verification 2026-09-15)*
- **This week specifically (2026-09-08 to 2026-09-15): fully quiet across all three
  sources.** Jira: 0 issues updated on board MP in the trailing 7 days. Slack: both
  channels scanned successfully (`ok: true` on both); every thread was a
  partner-support/customer-escalation question (SharePoint uni-directional sync ask from
  ING, Asana integration recommendation question, Jira-to-Bynder metadata sync question,
  Coolblue metaproperty/BigQuery sync failure, Figma Weave plugin support question, a new
  OneDrive integration sign-off for Rare Beauty, a Torino/Workflow support-routing
  question, a Kimia.ai MCP-vs-custom-integration question, and others) -- none referenced
  the four tracked features, and no messages came from Bas. Confluence: 0 pages in the
  INTEGRATE space modified since last Monday (2026-09-14); the three canonical feature
  pages (IAL Project Overview and Blueprint [5675221021], Certification Program Overview
  [5534351403], Partner Integrations & Connectors [1920630816]) are all unchanged from
  their last recorded versions. *(Source: Jira board MP; Slack #b-team-integrations,
  #b-help-global-partnerships; Confluence INTEGRATE space)*
- **Certification Program blockers persist:** Pencil.ai (MP-249) untouched since
  2026-08-12 -- now ~9 weeks stalled in Awaiting Certification since 2026-07-13.
  BrightCarbon (MP-266) was touched 2026-09-02 but stayed in Awaiting Certification --
  now ~6 weeks stalled since 2026-08-05. CloudCannon (MP-267) untouched since 2026-08-13
  -- now ~5 weeks stalled in Awaiting Certification. *(Source: Jira board MP)*
- **IAL, Doc Migration, Partner Onboarding:** no signal from any source since the last
  confirmed dates (IAL: 2026-07-21, ~8 weeks ago; Doc Migration / Partner Onboarding:
  2026-08-17 Confluence restructuring, ~4 weeks ago). feature-index.yaml left unchanged
  for these three per "do not update on absence of news." *(Source: absence of signal,
  cross-checked Jira/Slack/Confluence)*
- **Feature launch completeness check:** no Jira epics (issuetype = Epic) moved to
  Done/Released in the last 7 days -- nothing to flag. The five items that shipped in
  late August are child "Technology Partner Integration" issues under the still-Backlog
  Release Q3.2 (2026) epic (MP-253), not epics themselves, so they fall outside this
  check's epic-level scope. *(Source: Jira board MP)*

## Blockers

- **Pencil.ai (MP-249)** stalled in Awaiting Certification ~9 weeks (since 2026-07-13) --
  owner: Bas van Reeuwijk.
- **BrightCarbon (MP-266)** stalled in Awaiting Certification ~6 weeks (since 2026-08-05)
  -- owner: Bas van Reeuwijk.
- **CloudCannon (MP-267)** stalled in Awaiting Certification ~5 weeks (since 2026-08-13),
  untouched -- owner: Bas van Reeuwijk.
- **IAL pilot-adapter milestone** (target 2026-06-30) remains unconfirmed as complete or
  slipped, ~11 weeks overdue -- owner: Bas van Reeuwijk.
- **Doc Migration vs. Partner Onboarding ownership** -- which initiative owns the
  Confluence partner-directory restructuring (page 1920630816, raised 2026-08-17) is still
  unconfirmed by Bas, ~4 weeks outstanding -- owner: Bas van Reeuwijk.
- **Routine A2 pipeline paused** since 2026-08-20 (PR #7) -- three weekly syntheses
  (2026-08-25, 09-01, 09-08) are stuck unmerged; this cycle's branch will be a fourth
  unless the pipeline is re-enabled or PRs are opened manually -- owner: Toni Aquino
  (managing PR-opening manually per PR #7's description).

## Coming up

- Track the six newest Awaiting Certification items (Dyspatch, Bynder Bridge-WordPress,
  Veeva Vault/Klick, Tiled, Raspberry AI, Bynder DAM Connector-Umbraco) through to
  Awaiting Release / Released.
- Follow up with Bas on the continued Pencil.ai, BrightCarbon, and CloudCannon stalls.
- Confirm with Bas whether the Confluence partner-directory restructuring needs a Jira
  epic and which initiative (Doc Migration or Partner Onboarding) owns it -- still
  unresolved after multiple cycles.
- Decide whether to re-enable the Routine A2 cron for this squad or continue processing
  weekly-sync branches manually -- three cycles' worth are currently stuck.

## Features

| Feature | Status | Last signal |
|---|---|---|
| Integration Abstraction Layer | 🟡 In progress / some risk | No signal from Jira, Slack, or Confluence since 2026-07-21 (~8 weeks); 2026-06-30 pilot-adapter target now ~11 weeks overdue, unconfirmed (absence of signal, cross-checked Jira/Slack/Confluence) |
| Certification Program | 🟡 In progress | 2026-09-15 (Jira board MP, direct verification) -- 5 Release Q3.2 items RELEASED (MP-254, 257, 258, 260, 264, late Aug); 7 items in Awaiting Certification (MP-267, 269, 270, 271, 272, 273, 261); Pencil.ai (MP-249), BrightCarbon (MP-266), and CloudCannon (MP-267) all stalled; no Jira movement in the trailing 7 days |
| Doc Migration | 🟡 In progress / unconfirmed | No new signal since 2026-08-17 (~4 weeks; Confluence page 1920630816 v307, still current); last confirmed Jira wave remains 2026-07-13 (MP-242, Done); ownership vs. Partner Onboarding unresolved |
| Partner Onboarding | 🟡 In progress | No new signal since 2026-08-17 (~4 weeks; Confluence, INTEGRATE space, page 1920630816 v307, unchanged this week) |
