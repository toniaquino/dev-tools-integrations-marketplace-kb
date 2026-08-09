# engineering

## What is in this folder

- bug-investigations/: structured write-ups of past bugs and investigations
- RFCs/: request for comments documents for technical decisions

## Current state (as of 2026-06-20)

- No P0/P1 bugs found in INC board in the last 90 days.
- No RFCs found in Confluence INTEGRATE space. Add them here when created.
- bug-investigations/example-stub.md: format reference only, not a real investigation.

## When to read

- bug-investigations/: when investigating a new bug or checking if a similar issue
  has been seen before. Check this before starting any bug investigation.
- RFCs/: when making architecture decisions or reviewing past technical choices.

## Bug investigation format

All bug investigations follow the format in
.claude/writing-guides/bug-investigation-guide.md.

## RFC format

All RFCs follow the format in .claude/writing-guides/rfc-guide.md.

## Jira cross-reference

All bug investigations should reference their INC Jira ticket.
Run this JQL for P0/P1 bugs to seed new investigations:
project = INC AND issuetype = Bug AND priority in (Highest, High) ORDER BY updated DESC
