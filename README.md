# Crunchbase (crunchbase-data)

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
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

Crunchbase is a leading source of private and public company, funding, and investor data - firmographics, funding rounds, acquisitions, investors, people, and events across the global startup and business landscape. The **Crunchbase Data API (REST v4)**, at base `https://api.crunchbase.com/v4/data`, exposes this graph programmatically through four surfaces - Entity Lookup, Search, Autocomplete, and Deleted Entities (deltas) - for web intelligence, reference data, market research, sales and investment prospecting, and enrichment use cases.

It is a **read-only** RESTful service over HTTPS, authenticated with an API key passed either as the `user_key` query parameter or the `X-cb-user-key` header, and rate limited to **200 calls per minute**.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/crunchbase-data/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/crunchbase-data/refs/heads/main/apis.yml)

## Access Model (Important)

Crunchbase API access is **subscription-gated**. There is no free, self-serve full-API tier:

- **Enterprise License** - full Data API access to the complete graph; custom / contact-sales pricing (historically starting in the tens of thousands of dollars per year).
- **Applications License** - broad API access for embedding Crunchbase data in a product; custom / contact-sales pricing.
- **Basic API** - a reduced API surface available to holders of the paid **Crunchbase Basic** plan.

Standard Crunchbase web subscription tiers (Starter / Pro / Business) do **not** include full API access.

Because live API responses require a paid license, the **endpoint paths, HTTP methods, authentication, and rate limits** documented here are grounded in the public Crunchbase developer docs ([data.crunchbase.com/docs](https://data.crunchbase.com/docs)), while the **field-level request/response schemas** in the OpenAPI are honestly modeled from the documentation rather than captured from live calls (see `x-endpoints-modeled` in the OpenAPI).

## Tags

- Company Data
- Web Intelligence
- Funding Data
- Firmographics
- B2B Data
- Investor Data
- Reference Data
- Fortune 1000

## Timestamps

- **Created:** 2026-07-11
- **Modified:** 2026-07-11

## APIs

### Crunchbase Entity Lookup API

Retrieve a single entity from a core collection - organizations, people, funding_rounds, acquisitions, and more - by UUID or permalink, selecting fields with `field_ids` and related data with `card_ids`. `GET /entities/{collection}/{entity_id}` plus a card endpoint for paging past the 100-item inline card limit. Ideal for firmographic enrichment and company reference-data lookups.

- **Human URL:** [https://data.crunchbase.com/docs/using-entity-lookup-apis](https://data.crunchbase.com/docs/using-entity-lookup-apis)
- **Base URL:** `https://api.crunchbase.com/v4/data`

#### Tags

- Company Data
- Firmographics
- Reference Data

#### Properties

- [Documentation](https://data.crunchbase.com/docs/using-entity-lookup-apis)
- [API Reference](https://data.crunchbase.com/docs/using-the-api)
- [OpenAPI](openapi/crunchbase-data-openapi.yml)
- [Postman Collection](collections/crunchbase-data.postman_collection.json)
- [Open Collection](collections/crunchbase-data.opencollection.json)

### Crunchbase Search API

Query a collection (organizations, people, funding_rounds, acquisitions, and others) with a JSON body of `field_ids` and AND-combined query predicates. `POST /searches/{collection}` returns 50 items by default and up to 1000 per request, with keyset pagination via `after_id` / `before_id`. The workhorse for building targeted company lists, funding-data feeds, and web-intelligence datasets.

- **Human URL:** [https://data.crunchbase.com/docs/using-search-apis](https://data.crunchbase.com/docs/using-search-apis)
- **Base URL:** `https://api.crunchbase.com/v4/data`

#### Tags

- Web Intelligence
- Funding Data
- B2B Data

#### Properties

- [Documentation](https://data.crunchbase.com/docs/using-search-apis)
- [Examples](https://data.crunchbase.com/docs/examples-search-api)
- [OpenAPI](openapi/crunchbase-data-openapi.yml)
- [Postman Collection](collections/crunchbase-data.postman_collection.json)
- [Open Collection](collections/crunchbase-data.opencollection.json)

### Crunchbase Autocomplete API

Resolve a query string to matching entity identifiers, optionally scoped to collections such as `organization.companies`, `principal.investors`, or `categories`. `GET /autocompletes` (limit up to 25) is typically used to obtain the UUIDs or permalinks that feed downstream Search and Entity Lookup calls.

- **Human URL:** [https://data.crunchbase.com/docs/using-autocomplete-api](https://data.crunchbase.com/docs/using-autocomplete-api)
- **Base URL:** `https://api.crunchbase.com/v4/data`

#### Tags

- Autocomplete
- Company Data
- Reference Data

#### Properties

- [Documentation](https://data.crunchbase.com/docs/using-autocomplete-api)
- [Examples](https://data.crunchbase.com/docs/examples-autocomplete-api)
- [OpenAPI](openapi/crunchbase-data-openapi.yml)
- [Postman Collection](collections/crunchbase-data.postman_collection.json)
- [Open Collection](collections/crunchbase-data.opencollection.json)

### Crunchbase Deleted Entities API

Detect entities removed from the Crunchbase Graph (compliance, data-quality cleanup, inappropriate content) so consumers can reconcile their own databases - the delta / change-detection surface. `GET /deleted_entities` and `GET /deleted_entities/{collection_id}` with `collection_ids` filtering, `deleted_at_order` sorting, and `after_id` / `before_id` keyset pagination.

- **Human URL:** [https://data.crunchbase.com/docs/using-deleted-entities-api](https://data.crunchbase.com/docs/using-deleted-entities-api)
- **Base URL:** `https://api.crunchbase.com/v4/data`

#### Tags

- Deltas
- Data Sync
- Reference Data

#### Properties

- [Documentation](https://data.crunchbase.com/docs/using-deleted-entities-api)
- [OpenAPI](openapi/crunchbase-data-openapi.yml)
- [Postman Collection](collections/crunchbase-data.postman_collection.json)
- [Open Collection](collections/crunchbase-data.opencollection.json)

## Common Properties

- [Authentication](authentication/crunchbase-data-authentication.yml)
- [Domain Security](security/crunchbase-data-domain-security.yml)
- [LinkedIn](https://www.linkedin.com/company/crunchbase)
- [Website](https://www.crunchbase.com)
- [Documentation](https://data.crunchbase.com/docs)
- [Sign Up](https://about.crunchbase.com/crunchbase-api-application-form/)
- [Plans](plans/crunchbase-data-plans-pricing.yml)
- [Rate Limits](rate-limits/crunchbase-data-rate-limits.yml)
- [Fin Ops](finops/crunchbase-data-finops.yml)
- [Blog](https://about.crunchbase.com/blog/)

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
