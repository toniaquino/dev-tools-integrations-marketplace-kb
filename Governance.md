# Governance

Config source for this repo's own weekly status-sync routine (Routine 6), parsed at
runtime. Modeled on `content-variations-delivery-performance-kb/Governance.md`'s
Ownership map / Channel map pattern, scoped to this domain's three squads. Built
2026-08-19 alongside the Routine 6 port -- revisit once there's more real usage to
learn from (see the "Structure -- provisional" note in root `CLAUDE.md`).

## Ownership map

| Area | Domain owner (Team Vault) | Decisions.md owner | Notes |
|---|---|---|---|
| Connectors | Tony Smith | Tony Smith | |
| Integrations | Todd Willms | Todd Willms | |
| Technology Partners | Bas van Reeuwijk | Bas van Reeuwijk | Folder name is `02 Teams/Technology Partners/`; the old repo used the longer "Technology Partners & Marketplace" -- same squad, shortened here to match this repo's actual folder. |

Toni Aquino (GPM, domain oversight) is not a per-area recipient by default -- she
owns the domain but each squad's PM owns their own area's weekly notification, same
pattern as the Content Variations Team Vault.

## Channel map

| Area | Primary channel | Additional channels |
|---|---|---|
| Connectors | #team-connectors | #b-help-integrationshub, #b-team-integrations |
| Integrations | #api-team | #b-team-integrations |
| Technology Partners | #b-team-integrations | #b-help-global-partnerships |

`#b-team-integrations` is shared engineering discussion across all three squads --
scan it for every area, not just Technology Partners.

## Source priority rules

- Delivery status: Jira wins over Slack; the current `Status.md` is the baseline.
- Decisions: Slack wins (most recent explicit decision language); `Decisions.md` is
  the record once logged, not a source to re-derive from.
- Blockers: Slack wins; `Status.md`'s Blockers section is the record once logged.

Same rules as `content-variations-delivery-performance-kb/Governance.md` -- kept
identical intentionally so the two Team Vaults behave consistently.

## Squad repo map

Not applicable in this repo the way it is in `content-variations-delivery-performance-kb`.
There are no separate squad repos to connect to -- Connectors, Integrations, and
Technology Partners live directly under `02 Teams/` in this repo, and
Routine A/A2 (per squad, see `.github/workflows/routine-{connectors,integrations,techpartners}-a*.yml`)
already scan each squad's own Jira/Slack and maintain the detailed, per-feature
`Status.md` files under `02 Teams/<Squad>/product-development/`.

## Routine 6 -- weekly status sync (team-level rollup)

**Purpose:** a condensed, cross-squad-skimmable team-level `Status.md` per area
(`02 Teams/<Squad>/Status.md`), separate from and simpler than the detailed
per-feature `Status.md` files Routine A already maintains under each squad's
`product-development/` tree. Built 2026-08-19 for a future need (a domain owner
skimming across all three squads at a glance) even though current participation is
limited to three single-area owners -- see `.github/prompts/routine-6.md`.

**Cadence:** weekly, matching the source repo's original slot (Mondays 8:00 AM PT).

**Notification model:** direct Slack DM per owner, no shared digest-manifest system.
`content-variations-delivery-performance-kb`'s Routine 9 digest-batching exists
because that domain has ~6 owners who could each get pinged multiple times a week
across several routines; this domain has 3 owners with exactly one area each, so a
same-run direct DM has no batching problem to solve. Do not port Routine 9 here
unless that changes.

**PR reviewer:** the area's own domain owner from the Ownership map above (GitHub
username from each squad's `02 Teams/<Squad>/CLAUDE.md` team table), falling back to
`toniaquino` if unset.

## Confluence seed (cross-repo, sourced from content-variations-delivery-performance-kb)

Confluence-seed generation for Connectors and Technology Partners
(publishing to the `INTEGRATE` Confluence space) is **not** run from this repo. It
stays in `content-variations-delivery-performance-kb` as Routine 8 / 8B, using the
Atlassian/Confluence credentials already configured there -- deliberately not
duplicated into this repo's secrets (2026-08-19 decision).

As of 2026-08-19, Routine 8 reads its Connectors / Technology Partners source
content (`Status.md`, `Decisions.md`, `Partner Integrations.md`) from **this repo**
via the GitHub Contents API (`GET /repos/toniaquino/dev-tools-integrations-marketplace-kb/contents/...`,
using the `GH_PAT` already present in both repos' secrets -- not a new or shared
credential, the same identity already used for every routine in this fleet), instead
of from now-stale local copies in its own repo. This repo is the source of truth for
those three files going forward:

- `02 Teams/Connectors/Status.md` -- written by this repo's own Routine 6.
- `02 Teams/Connectors/Decisions.md` -- human-maintained (via the `decision-logger`
  skill or direct edit), seeded 2026-08-19 from the old repo's archived copy.
- `02 Teams/Connectors/Partner Integrations.md` -- human-maintained, seeded
  2026-08-19 from the old repo's archived copy.
- `02 Teams/Technology Partners/Status.md` -- written by this repo's own Routine 6.
- `02 Teams/Technology Partners/Decisions.md` -- human-maintained, seeded 2026-08-19.

Edit these files here going forward, not in `content-variations-delivery-performance-kb`
-- that repo's copies are frozen historical snapshots (see the ARCHIVED banner on
each).
