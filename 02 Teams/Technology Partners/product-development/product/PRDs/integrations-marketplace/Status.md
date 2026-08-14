# Integrations Marketplace -- status

**Last updated:** 2026-08-14
**PM:** Bas van Reeuwijk
**Status:** 🟡

## This week

- **Doc Migration -- next wave now confirmed in progress:** Bas van Reeuwijk corrected
  Jira descriptions for three Release Q3.2 partner integrations against their original
  intake forms on 2026-08-11 -- FADEL (MP-257) was previously misattributed to "The DAM
  Consultants" as implementation partner, corrected to Gournay Consulting; FLUiiD4
  (MP-260)'s description didn't match the submitted intake and was rewritten;
  Brandfolder Migration Tool (MP-258) went from no description to a full one. Each
  ticket also gained a linked Confluence page. This was followed by a much larger
  sweep: 143 pages across the INTEGRATE space were rewritten/restructured by Bas van
  Reeuwijk in a single ~2.5-hour session on 2026-08-13 (13:22-15:55 CEST), standardizing
  partner-page templates (structured status badges, disambiguation entries for
  same-named integrations, richer partner/commercial/onboarding sections). No Jira epic
  currently tracks this wave -- the prior wave was MP-242 (Done 2026-07-13); this one so
  far exists only as direct page/ticket edits. *(Source: Jira board MP -- MP-257,
  MP-258, MP-260 changelogs; Confluence INTEGRATE space, 143 pages diffed by version)*
- **Certification pipeline -- active movement on Release Q3.2 (MP-253):** Corsearch
  (MP-254) advanced Training Material Complete -> Awaiting Release (2026-08-12), the
  closest item in the current wave to shipping. Fadel/Gournay Consulting (MP-257)
  reached Training Material Complete (2026-08-11). Brandfolder Migration Tool (MP-258)
  and Fluiid4/CLX Europe (MP-260) both entered Awaiting Certification (2026-08-11) --
  Brandfolder had been IN REVIEW per last week's Confluence signal, so Jira now shows it
  a step further along. *(Source: Jira board MP)*
- **New release wave opened -- Q4.1 (2026):** Epic MP-259 appeared with its first
  entrant, the Bynder-CloudCannon integration (MP-267), which moved Backlog -> Awaiting
  Certification on 2026-08-13. *(Source: Jira board MP)*
- **Pencil.ai (MP-249) unparented from Release Q3.2:** Still Awaiting Certification
  (unchanged since 2026-07-13, ~4.5 weeks stalled), but its Jira parent link to MP-253
  was removed by Bas van Reeuwijk on 2026-08-12. Reason not stated in Jira -- flagged
  below, needs a PM check. *(Source: Jira board MP, issue changelog)*
- **Integration Abstraction Layer:** No signal from any source again this cycle -- none
  of the 7 Jira issues updated this week relate to IAL, no Slack mentions, and the IAL
  blueprint/RFC Confluence page was not among the 143 pages touched this week. Streak
  continues from 2026-07-21; the 2026-06-30 pilot-adapter target is now 6+ weeks
  overdue, still unconfirmed as complete or slipped. *(Source: absence of signal,
  cross-checked Jira/Slack/Confluence)*
- **Slack:** Both channels scanned successfully (25 messages in #b-team-integrations, 2
  in #b-help-global-partnerships). All were partner-support/customer-escalation threads
  (Adobe CC/LinkrUI security-certificate issue at WCLC, Hilti webhook/cross-account AWS
  blocker, ChatGPT OAuth blocker for ABM, MCP access requests, a new Arla lead, and
  others) -- no PM-level decisions or blockers touching the four tracked features.
  *(Source: Slack #b-team-integrations, #b-help-global-partnerships)*

## Blockers

- **IAL pilot-adapter milestone** (target 2026-06-30) now 6+ weeks overdue and
  unconfirmed -- owner: Bas van Reeuwijk.
- **Pencil.ai (MP-249)** stalled in Awaiting Certification since 2026-07-13 (~4.5
  weeks) and now also unparented from Release Q3.2 -- owner: Bas van Reeuwijk. Needs
  clarification on whether it's being reassigned to a different release wave or
  deprioritized.
- **Doc Migration wave has no Jira epic** -- the 143-page Confluence sweep and the
  three corrected partner tickets aren't tracked under any epic, unlike the Q3.1 wave
  (MP-242). Recommend opening one so this wave's completeness can be checked the way
  Q3.1's was.

## Coming up

- Watch Corsearch (MP-254) through to Awaiting Release -> Released -- closest item in
  the current wave.
- Track Brandfolder Migration Tool (MP-258) and Fluiid4 (MP-260) through certification
  now that both have entered Awaiting Certification.
- Watch the new Q4.1 (2026) wave (MP-259) for further entrants beyond CloudCannon
  (MP-267).

## Features

| Feature | Status | Last signal |
|---|---|---|
| Integration Abstraction Layer | 🟡 In progress / some risk | No fresher signal since 2026-07-21; 2026-06-30 pilot-adapter target now 6+ weeks overdue, unconfirmed (Source: absence of signal, cross-checked Jira/Slack/Confluence) |
| Certification Program | 🟡 In progress -- active this week | 2026-08-12 (Jira board MP) -- Corsearch (MP-254) reached Awaiting Release; Fadel (MP-257) reached Training Material Complete; Brandfolder (MP-258) and Fluiid4 (MP-260) entered Awaiting Certification; Pencil.ai (MP-249) still stalled and now unparented from MP-253 |
| Doc Migration | 🟢 On track -- next wave confirmed in progress | 2026-08-13 (Confluence INTEGRATE space, 143 pages) + 2026-08-11 (Jira MP-257/258/260 description corrections) -- no epic yet tracking this wave |
| Partner Onboarding | 🟢 Active | 2026-08-03 (Confluence, Partner Integrations & Connectors page) unchanged this week -- only an incidental link-version bump on 2026-08-12 from the wider page rewrite, no new tracker entries |
