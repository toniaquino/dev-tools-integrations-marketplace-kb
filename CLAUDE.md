# Dev Tools / Integrations / Marketplace Vault

This is Toni's **horizontal-domain Team Vault** — the team brain for the Dev
Tools / Integrations / Marketplace domain (Tech Partners & Marketplace, Connectors,
API Extensibility/Integrations), parallel to `content-variations-delivery-performance-kb`
(her core Content Variations & Delivery domain). One rung below the cross-GPM
**Product Vault** (`product-team-kb`), one rung above her personal `toni-vault`.

> **Mental model:** part of Toni's team brain — a team-level extension of the
> PARA-based second-brain method, not a static reference library. Full explanation
> in `product-team-kb/CLAUDE.md` (the Product Vault).

## What this repo is

Canonical source of current state for this domain's squads (Tech Partners,
Connectors, Integrations), their initiatives, teams, and decisions.
Primary consumer: Claude AI agents. Human readability is a design constraint.

## Structure — provisional, revisit before treating as final

```
02 Teams/
  Technology Partners/   product-development/ + team/, migrated from tech-partners-squad-kb
  Connectors/             product-development/ + team/, migrated from connectors-squad-kb
  Integrations/           product-development/ + team/, migrated from integrations-squad-kb
```

**This structure was created by copying the pattern from
`content-variations-delivery-performance-kb` (`02 Teams/<Squad>/`) without a
dedicated design pass for this domain specifically** — that Team Vault's structure
evolved organically over several PARA-based iterations; this one was scaffolded in
one sitting to get real content migrated. In particular, unlike the Content
Variations Team Vault, this domain has no `01 Initiatives/` layer yet (Integrations
Marketplace and API Extensibility exist as squad-level initiatives inside each
squad's own `feature-index.yaml`, not elevated here), and no cross-program or
customer-notes folders. Revisit this structure once there's more real usage to learn
from, rather than assuming the Content Variations layout is automatically right for
a domain with different squad-ownership dynamics (this domain's three squads don't
share a single initiative-owner/squad-PO split the way Deliver or Organize do).

## Team members

| Name | Role | Slack ID | GitHub |
|---|---|---|---|
| Toni Aquino | GPM (owner) | U9ATXKJM6 | toniaquino |
| Bas van Reeuwijk | PM, Technology Partners & Marketplace | U04H9D3H14K | [TBD] |
| Tony Smith | PM, Connectors | UPQ9D0BFX | tonysmith-ux |
| Todd Willms | PM, Integrations | U01EHRXEBFE | twillmsbynder |

## Key channels

- `#b-team-integrations`: shared engineering channel across all three squads
- `#team-connectors`, `#api-team`, `#b-team-integrations` (Tech Partners' main
  channel): squad-specific, see each squad's own `CLAUDE.md` under `02 Teams/`

## What does not belong here

Personal notes, meeting transcripts, full Confluence reproductions, draft thinking.
Link to source; do not reproduce. Same rule as the Content Variations Team Vault.

## Routine config

- PR reviewer: `toniaquino`
