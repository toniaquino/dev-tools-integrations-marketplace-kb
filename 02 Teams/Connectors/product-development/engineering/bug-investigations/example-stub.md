# STUB: No P0/P1 bugs found in last 90 days -- example format only
# Format: see .claude/writing-guides/bug-investigation-guide.md
# When a real bug investigation is needed, copy this file, rename it
# YYYY-MM-DD-[INC-KEY]-[short-description].md, and fill in all sections.

# BUG: [Short description] -- YYYY-MM-DD

**Jira ticket:** [INC-KEY]
**Severity:** [P0 / P1 / P2 / P3]
**Reported by:** [Name or team]
**Investigated by:** [Name]
**Status:** [Open / Resolved / Closed as won't fix]

---

## What happened

[Clear description of the bug. What was the user doing? What was the expected
behavior? What happened instead?]

## Reproduction steps

1. [Step 1]
2. [Step 2]
3. [Step 3 -- observed result]

## Scope

[How many users or customers affected? What integration surface? What environments?]

## Root cause

[What caused this? Be specific about the code path, service, or connector involved.]

## Fix applied

[What was changed to fix it? PR or commit reference.]

## Infrastructure touched

[Which services, connector APIs, or systems were involved?]

## Resolution

[YYYY-MM-DD: How it was resolved.]

## Lessons learned

[What would prevent this in future? Any monitoring or alerting gaps?]
