# Partner Integrations

> **Seeded 2026-08-19** from `content-variations-delivery-performance-kb`'s archived
> copy (that repo's copy is now a frozen historical snapshot — see its ARCHIVED
> banner). This is the live copy going forward; edit here, not there. Read by Routine
> 8 in `content-variations-delivery-performance-kb` via cross-repo API — see this
> repo's `Governance.md` → "Confluence seed".

Structured metadata for Connectors' active technology-partner integrations. One section per partner.

## Integration ownership models

Two distinct models show up across active integrations -- get this right before filing a new entry:

- **Bynder-owned integration:** Bynder holds a direct strategic commercial partnership with the platform, and the integration itself is built and maintained by a separately contracted development partner. Salesforce is the reference example, with a different development partner per product surface: CobraCRM builds DAM Connect, LWC, and Data Cloud; Royal Cyber builds Salesforce Commerce Cloud; Penfield Digital (now Assist NL) builds Salesforce Marketing Cloud. Contentful follows the same pattern, with Appnovation as the development partner. Full Salesforce / Strategic Integrations tracking lives in `02 Teams/Integrations/`, not here.
- **Partner-built integration:** the technology partner's own ecosystem builds and lists the connector directly (e.g. Akeneo, built by Dataggo).

## Contentful

**Type:** Bynder-owned integration on the Bynder Marketplace -- same ownership pattern as Salesforce (see "Integration ownership models" above): Bynder holds the strategic commercial partnership with Contentful directly, and Appnovation is the contracted development partner who builds and maintains the integration. Not a partner-built integration like Akeneo/Dataggo.
**Category:** CMS (Content Management System)
**Connector built by:** Appnovation (contracted, Bynder-owned integration; not Contentful-built or Contentful-listed)
**Bynder Marketplace listing:** not confirmed -- check with Tony Smith / Bas van Reeuwijk before citing a listing status
**Relationship owner (partnership side):** Meghan Dussault (Partnerships)
**Relevant initiatives:** connectors (Contentful integration), genai-transformation-agent (CMS-injection-point open question)
**Status (as of 2026-07-17):** The Appnovation-built integration itself was last reforecast as on hold (2026-07-03 vendor budget review, no timeline from Appnovation's Megan) pending the Salesforce/Contentful acquisition close. Separately, and more recently, the Contentful *partnership* conversation is active and forward-looking, not paused -- corrects a framing that had spread internally describing the relationship overall as "on hold, may be killed." The acquisition itself has not yet closed (targeted first week of September 2026, pending regulatory approval); Contentful's own product-level planning is genuinely constrained until then, but the partnership conversation is continuing regardless of the integration-build status.

### Current state
- Bynder's DAM Connect (asset-picker/external-provider model) was overtaken by Salesforce's pivot to Data 360 before Bynder finished building against it. Bynder's structured-data / CX Omnichannel reference-URL approach may converge with where things are headed, given a shared interest in agentic, API-level integration that bypasses the Data 360 layer entirely.
- MCP interoperability is the most concrete near-term opportunity. Contentful already has a live (unannounced) remote MCP server; Bynder has one in the same soft-launch state. An agent orchestrating across both was floated as a demo story -- real, partner-originated validation for Bynder's own MCP use case.
- Federated search across Contentful-native and Bynder-hosted assets is a real ask from Contentful, not yet solved. Bynder's AI search improvements help within Bynder's own views but don't solve cross-system federation.
- Native-app precedent: an earlier UCV-as-native-app build inside Adobe's GenStudio framework is a possible model for a "Contentful app," as an alternative to the current iframe/compact-view integration.
- Open question from Bynder's side: where in a customer's CMS workflow Bynder's GenAI/Transformation Agent capabilities should trigger. Bynder doesn't have enough visibility into customer content-editing workflows to answer this alone.
- Contentful is a confirmed gold sponsor with a speaking slot at Bynder Connect, Sept 9-10, Amsterdam.
- FIFA is a joint reference account (media/photo selection for publishers); integration is relatively basic, no known issues.

### Commercial context
- Appnovation is one of several contracted integration-build vendors tracked in Connectors' vendor budget (alongside MD Systems, Geta, Royal Cyber). Last reforecast 2026-07-03: still on hold post-Salesforce-acquisition-announcement, no timeline given, reforecast unchanged.
- This is a cost/vendor-management track, independent of the partnership-relationship track above -- the integration build being on hold doesn't mean the partner relationship is paused, and vice versa. Keep the two straight when reporting status.

### Key contacts
| Name | Org | Role |
|---|---|---|
| Erin Keefe | Contentful | Solution Partner Manager |
| Adam Weinstein | Contentful | Lead, Product Partnerships |
| Zachary Yankiver | Contentful | PM, Applied AI Solutions + Marketplace/Extensibility |
| Meghan Dussault | Bynder | Partnerships, relationship owner |

### Open items
- [ ] Correct the "on hold, may be killed" framing wherever else it appears in team materials
- [ ] Schedule a more technical follow-up call once Contentful's enablement material lands (expected end of July 2026)
- [ ] Support Contentful's Bynder Connect session/demo content given the sponsorship

### Log
- 2026-07-17 | Bynder x Contentful: Use Cases + Integration Roadmap | First substantive strategic call on this relationship. Covered Salesforce acquisition status, FIFA recap, search/video roadmap, and the MCP interoperability opportunity.
