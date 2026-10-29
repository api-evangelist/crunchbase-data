# Crunchbase

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

Crunchbase is a leading source of private and public company, funding, and investor data - firmographics, funding rounds, acquisitions, investors, people, events, and AI-generated predictions and insights across the global startup and business landscape. The Crunchbase Data API (REST v4, base https://api.crunchbase.com/v4/data) exposes this graph programmatically through Entity Lookup, Search, Autocomplete, and Deleted Entities across 43 entity collections, and is published as six package-scoped OpenAPI 3.0.1 documents - Firmographic, Core Financials, Advanced Financials, Insights, Predictions, and Predictions & Insights - discoverable through an RFC 9727 api-catalog at data.crunchbase.com. Crunchbase also ships a first-party remote MCP server at mcp.crunchbase.com over Streamable HTTP with fourteen documented tools, authenticated with OAuth 2.1 + PKCE and sold as per-user MCP seats. The REST API is read-only and authenticated with a single account-level API key (user_key query parameter or X-cb-user-key header); which of the six packages that key is provisioned against determines which operations it can call. Access is subscription-gated with no published pricing - the full API requires a Crunchbase Enterprise or Applications licence, with a reduced Basic API for Crunchbase Basic plan holders.

**Areas:** Company Data · Web Intelligence · Funding Data · Firmographics · B2B Data · investor-data · Reference Data · Private Markets · Predictions · Market Insights · MCP · Fortune 1000

## Crunchbase on APIs.io

Everything profiled for Crunchbase is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/crunchbase-data/](https://apis.io/providers/crunchbase-data/)** — or go straight to one of the APIs or properties below.

### APIs (6)

- [Crunchbase MCP Server](https://apis.io/apis/crunchbase-data/crunchbase-data-mcp/) — First-party remote Model Context Protocol server over Streamable HTTP, exposing fourteen tools - five natural-language expert tools, four structured…
- [Crunchbase Autocomplete API](https://apis.io/apis/crunchbase-data/crunchbase-data-autocomplete-api/) — The Autocomplete API from Crunchbase — 1 operation(s) for autocomplete.
- [Crunchbase Deleted Entities API](https://apis.io/apis/crunchbase-data/crunchbase-data-deleted-entities-api/) — The Deleted Entities API from Crunchbase — 2 operation(s) for deleted entities.
- [Crunchbase Entity API](https://apis.io/apis/crunchbase-data/crunchbase-data-entity-api/) — The Entity API from Crunchbase — 60 operation(s) for entity.
- [Crunchbase Metadata API](https://apis.io/apis/crunchbase-data/crunchbase-data-metadata-api/) — The Metadata API from Crunchbase — 3 operation(s) for metadata.
- [Crunchbase Search API](https://apis.io/apis/crunchbase-data/crunchbase-data-search-api/) — The Search API from Crunchbase — 43 operation(s) for search.

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [Crunchbase](https://apis.io/servers/crunchbase-data/crunchbase/)

#### Agentic access (1)

Which operations an agent can call, which act, and which need a human in the loop.

- [Crunchbase Data Agentic Access](https://apis.io/agentic-access/crunchbase-data/crunchbase-data-agentic-access/)

#### Collections (5)

Postman and Open Collection request collections.

- [Crunchbase Data API v4](https://apis.io/collections/crunchbase-data/open-crunchbase-data/)
- [Crunchbase Data API v4 Autocomplete API](https://apis.io/collections/crunchbase-data/open-crunchbase-data-autocomplete-api/)
- [Crunchbase Data API v4 Autocomplete Deleted Entities API](https://apis.io/collections/crunchbase-data/open-crunchbase-data-deleted-entities-api/)
- [Crunchbase Data API v4 Autocomplete Entity Lookup API](https://apis.io/collections/crunchbase-data/open-crunchbase-data-entity-lookup-api/)
- [Crunchbase Data API v4 Autocomplete Search API](https://apis.io/collections/crunchbase-data/open-crunchbase-data-search-api/)

#### Overlays (6)

OpenAPI overlays, including conversational phrasing for each operation.

- [Crunchbase Data Advanced Financials Overlay](https://apis.io/overlays/crunchbase-data/crunchbase-data-advanced-financials-overlay/)
- [Crunchbase Data Core Financials Overlay](https://apis.io/overlays/crunchbase-data/crunchbase-data-core-financials-overlay/)
- [Crunchbase Data Firmographic Overlay](https://apis.io/overlays/crunchbase-data/crunchbase-data-firmographic-overlay/)
- [Crunchbase Data Insights Overlay](https://apis.io/overlays/crunchbase-data/crunchbase-data-insights-overlay/)
- [Crunchbase Data Predictions Insights Overlay](https://apis.io/overlays/crunchbase-data/crunchbase-data-predictions-insights-overlay/)
- [Crunchbase Data Predictions Overlay](https://apis.io/overlays/crunchbase-data/crunchbase-data-predictions-overlay/)

#### Security (3)

Authentication, trust centre, and vulnerability disclosure.

- [Crunchbase Data Authentication](https://apis.io/security/crunchbase-data/crunchbase-data-authentication/)
- [Crunchbase Data Domain Security](https://apis.io/security/crunchbase-data/crunchbase-data-domain-security/)
- [Crunchbase Data Vulnerability Disclosure](https://apis.io/security/crunchbase-data/crunchbase-data-vulnerability-disclosure/)

#### OAuth scopes (1)

The permissions the API asks for.

- [Crunchbase Data Scopes](https://apis.io/scopes/crunchbase-data/crunchbase-data-scopes/)

#### Plans and pricing (1)

Published plans, tiers and prices.

- [Crunchbase Data Plans Pricing](https://apis.io/plans/crunchbase-data/crunchbase-data-plans-pricing/)

#### Rate limits (1)

Published request limits.

- [Crunchbase Data Rate Limits](https://apis.io/rate-limits/crunchbase-data/crunchbase-data-rate-limits/)

#### FinOps (1)

What the API costs to run, by operation.

- [Crunchbase Data Finops](https://apis.io/finops/crunchbase-data/crunchbase-data-finops/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://www.crunchbase.com)
- [Documentation](https://data.crunchbase.com/docs)
- [Getting started](https://data.crunchbase.com/docs/welcome-to-crunchbase-data)
- [API reference](https://data.crunchbase.com/reference)
- [Pricing](https://about.crunchbase.com/pricing/)
- [Sign up](https://about.crunchbase.com/products/crunchbase-api/)
- [Changelog](https://about.crunchbase.com/product-updates/)
- [Blog](https://about.crunchbase.com/blog/)
- [Security](https://www.crunchbase.com/.well-known/security-policy.html)
- [Terms of service](https://about.crunchbase.com/terms-of-service/)
- [Privacy policy](https://about.crunchbase.com/privacy-policy/)
- [GitHub](https://github.com/crunchbase)

## API Evangelist rating

**Kin Score 48.4** — developing · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 80.0 |
| Contract quality | 22.8 |
| Contract governance | 4.5 |
| Operational transparency | 60.5 |
| Developer ergonomics | 39.9 |
| Access clarity | 76.3 |

**Agent readiness 46.0** — agent-ready (gated down from agent-native)

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | derived (partial credit) |
| Reversibility Documented | — |
| MCP Server | verified |
| Auth Clarity | served (partial credit) |
| Idempotency | — |
| Error Semantics | derived (partial credit) |
| OpenAPI Examples | — |
| Rate Limit Signal | documented (partial credit) |
| Event Surface Described | — |
| Agent Skills | derived (partial credit) |
| Well Known Catalog | yes |
| Consent Identity | — |
| Agent Card | — |
| Dry Run Mode | — |
| Delegated Identity | served (partial credit) |
| Protected Resource Metadata | verified |
| Dynamic Client Registration | — |
| Agentic Commerce | — |
| Pagination Ratio | na |
| Operation Distinctiveness | distinct |

**Regulatory alignment 40.2** — Horizontal (data, software, accessibility, platform)

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/crunchbase-data/](https://apis.io/providers/crunchbase-data/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for Crunchbase: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/crunchbase-data/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
