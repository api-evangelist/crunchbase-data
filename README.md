# Crunchbase (crunchbase-data)

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
