# Connectors Squad Team OS — quick reference for Bill Keiffer (Solutions Architect)

**Repo:** https://github.com/toniaquino/connectors-squad-kb
**PM:** Tony Smith (@tony.smith on Slack)
**GPM:** Toni Aquino (@toni on Slack)

---

## Your contribution areas

1. **Bug investigations** (`product-development/engineering/bug-investigations/`)
   When you close a significant integration bug (P0/P1, or anything that took >2 hours to diagnose),
   write it up. Saves the next person hours. Especially valuable for connector-specific failure modes
   that aren't obvious from Jira tickets alone.

2. **RFCs** (`product-development/engineering/RFCs/`)
   When you make an architecture or integration design decision — a new i-Hub pattern,
   connector authentication approach, Tray configuration decision — write an RFC.
   If it already lives in Confluence, create a stub here that links to it.

3. **Feature index updates** (`product-development/product/feature-index.yaml`)
   When a feature you're delivering ships, update its status field to ✅ Shipped
   and fill in any artifact paths (PRD, Figma, customer context) that are still tonysmith-ux.

---

## How to contribute

1. **Preferred:** Paste your write-up in #b-help-integrationshub and tag @tony.smith or @toni
   — they'll format and commit it for you. You don't need GitHub access.
2. **Direct:** If you have GitHub access, open a PR to this repo and tag Tony as reviewer.
3. Format: use `.claude/writing-guides/bug-investigation-guide.md` or `rfc-guide.md` as templates.

---

## Writing guides for your role

| Guide | When to use |
|---|---|
| `.claude/writing-guides/bug-investigation-guide.md` | After closing a significant connector bug |
| `.claude/writing-guides/rfc-guide.md` | Before/after a significant technical decision |

---

## Key files you'll interact with

| File | What it is |
|---|---|
| `product-development/product/feature-index.yaml` | Master lookup — all features, their Jira keys, artifact paths |
| `product-development/engineering/bug-investigations/` | Past bug write-ups — check here before diagnosing |
| `product-development/engineering/RFCs/` | Architecture decisions |
| `product-development/product/competitive-research/partner-integrations-overview.md` | Full catalog of available integrations |

---

## Questions

Ask in #b-help-integrationshub or DM @tony.smith / @toni directly.
