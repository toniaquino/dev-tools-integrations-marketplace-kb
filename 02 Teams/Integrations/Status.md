# Integrations

**Status:** 🟡 At risk — shipped a major UCV release and broad harnessing work is progressing, but a webhook workstream is blocked on DevOps.
**Last updated:** 2026-08-31
**Last reviewed:** 2026-08-31
**Review due:** 2026-09-14
**Owner:** Todd Willms
**Source channels:** #api-team (not found in Slack — see note below), #b-team-integrations

> Note: #api-team could not be resolved via the Slack API this run (not returned by
> `conversations.list`, or a private channel this bot isn't a member of —
> indistinguishable from our side). Only #b-team-integrations was scanned. Flagged for
> the domain owner to confirm the channel name/membership.

## Current state
- Released a new major UCV version this week (API-2839, Done).
- Broad SDK "harnessing" / resumable-upload initiative underway across Java, Python,
  PHP, and C# (API-2770/2771/2772/2773 resumable uploads; API-2775/2776/2777/2778/2759/2787/2786/2768
  harness creation and investigation) — Python harness already done (API-2776), rest
  in progress or to do.
- UCV work: isArchived filtering in code review (API-2352, API-2597) with a follow-up
  FE task still to do (API-2610); SmartFilters performance improvements queued
  (API-2819, Backlog); GenAI Smartedit POC completed (API-2854, Done) with a related
  GenAI investigation still in progress (API-2741).
- Observability: Honeycomb tracing spikes in progress for webhooks and UCV logging
  (API-2695, API-2823).
- Moving Rabobank to the new Webhooks UI (API-2852, To Do); setting up an Integrations
  team skills repo (API-2887, To Do).

## Blockers
- SNS webhook SignatureVersion-2 (SHA-256) update is blocked: the team does not
  currently have sufficient permissions and has asked DevOps for help (source: Slack
  #b-team-integrations, 2026-08-25). Related tickets API-2864 and API-2889 are still
  To Do/Backlog in Jira, which does not itself show a "blocked" state — flagging this
  as a source conflict per Governance.md's priority rules (Slack wins on blockers).
