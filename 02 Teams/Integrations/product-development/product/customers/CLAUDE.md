# customers

## What is in this folder

One subfolder per key customer account or segment.
Each contains: a summary.md (key contacts, segment, account context)
and a calls/ subfolder with individual Gong call summaries.

## Customer context for Integrations squad

The Integrations squad builds platform APIs (UCV, Webhooks, OAuth) consumed by:

1. **Integration partners** — ISVs and agencies building Bynder connectors into CMS,
   e-commerce, creative tools (e.g. Sitecore, Contentful connectors, custom DAM
   integrations). Primary stakeholders in UCV and Webhooks roadmap.

2. **Enterprise customers with custom integrations** — customers who built their own
   integrations using Bynder's public API. Main migration audience for /compact
   deprecation (API-2677) and OAuth1 deprecation (API-2463).

3. **Developers** — individual developers using Bynder's API and SDKs. Primary
   audience for AI/Agentic track (API-2743, API-2744).

No named customer accounts were identified at seed time (2026-06-19).
Add named accounts here as Gong call summaries are imported.

## Key accounts

| Account | Segment | Subfolder |
|---|---|---|
| [FILL IN — add named accounts as calls are imported] | | |

## When to read

- summary.md: for account context, key contacts, or relationship history
- calls/: for specific call content or synthesis across calls
- Do not load all call summaries for a general customer query —
  read summary.md first. Go into calls/ only if summary does not have what you need.

## Adding Gong transcripts

No Gong MCP is available yet. To add a call summary:
1. Export the transcript from Gong manually
2. Upload the file to the relevant customer subfolder under calls/
3. Run the customer-call-guide.md skill to reformat it into the standard structure

## Call summary format

All call summaries follow the format in .claude/writing-guides/customer-call-guide.md.

## Adding a new customer account

Create a subfolder with summary.md and calls/CLAUDE.md.
Update this CLAUDE.md key accounts table.
Update root CLAUDE.md doc index if a new major segment is added.
