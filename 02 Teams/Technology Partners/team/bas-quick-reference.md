# Squad Team OS — quick reference for Bas van Reeuwijk (PM, Technology Partners)

**Repo:** https://github.com/tonicaquino-ai/tonicaquino-ai-tech-partners-squad-kb
**Acting PM:** Toni Aquino — DM on Slack for repo questions
**Your Slack:** <@U04H9D3H14K>

---

## Your role in this repo

You are the primary contributor. The repo captures your squad's product knowledge —
partner context, integration status, decisions, and strategy — so it stays accessible
to you and to AI agents working on your behalf, without relying on your memory or
Slack history.

External tech partners do not contribute to the repo directly. You capture their
context after calls and meetings.

---

## What you contribute and when

### After a partner call or meeting
**Where:** `product-development/product/customers/[partner-name]/`
**Format:** `.claude/writing-guides/customer-call-guide.md`
**How:** Commit directly or open a PR. If it's a quick note, paste in `#b-team-integrations` and tag Toni — she'll commit it.

One habit that makes this work: write the summary while the call is still fresh.
The call guide takes 10 minutes. It saves hours when the same partner comes up in
a future planning cycle.

### When integration status changes
**Where:** `product-development/product/feature-index.yaml`
**What:** Update the `status` field for the relevant feature. Add a `last_updated` note if meaningful context changed.
**How:** Direct commit on `main` (no PR needed for status-only updates).

There is no Jira board for this squad. `feature-index.yaml` is the authoritative
record of what is in flight, what shipped, and what is blocked. Keep it current.

### When a partner or product decision is made
**Where:** `product-development/product/PRDs/integrations-marketplace/CLAUDE.md` (for initiative-level decisions) or a new `Decisions.md` in the relevant subfolder
**Format:** One decision per entry — date, decision, rationale, owner.
**How:** Direct commit or PR.

### When strategy shifts
**Where:** `product-development/product/strategy/marketplace-strategy.md`
**How:** Open a PR so there is a record of the change. One-line summary in the PR title is enough.

### Weekly status (auto-generated)
Routine A runs every Monday and opens a draft PR with an updated status summary sourced
from Slack and Confluence. Your job: review the PR, correct anything wrong, mark ready
to merge. You do not need to write Status.md manually — the routine handles it.

---

## Contribution paths

| Task | Path | Notes |
|---|---|---|
| Partner call summary | Direct commit to `customers/` or paste in Slack | Tag Toni if using Slack path |
| Feature status update | Direct commit to `feature-index.yaml` | No PR needed for status-only |
| Decision | Direct commit to relevant `Decisions.md` | Date + rationale required |
| Strategy update | PR | Keeps a change record |
| Weekly status | Review and merge Routine A draft PR | Routine opens it every Monday |

---

## Writing guides for your role

- **Partner call summary:** `.claude/writing-guides/customer-call-guide.md`
- **PRDs:** `.claude/writing-guides/prd-guide.md`
- **Strategy docs:** `.claude/writing-guides/strategy-doc-guide.md`
- **Your voice settings:** `.claude/pm-voice-guide.md` — customise before your first AI-assisted doc

---

## Key files

| File | What it is |
|---|---|
| `CLAUDE.md` (root) | Team roster, channels, initiative index |
| `product-development/product/feature-index.yaml` | Master integration status tracker |
| `product-development/product/strategy/marketplace-strategy.md` | Current strategy doc |
| `product-development/product/PRDs/integrations-marketplace/prd.md` | Initiative PRD |
| `product-development/engineering/RFCs/2025-11-27-integration-abstraction-layer-rfc.md` | IAL RFC |
| `product-development/product/customers/` | Partner context folder |

---

## What this repo does not replace

- Confluence: long-form reference docs, specs, and blueprints stay there. The repo links to them.
- Slack: async decisions and blockers surface in Slack first. The routine captures them here weekly.
- Gong: call recordings stay in Gong. The repo stores your written summaries.

---

## Questions

DM Toni on Slack (`U9ATXKJM6`) or ask in `#b-team-integrations`.
