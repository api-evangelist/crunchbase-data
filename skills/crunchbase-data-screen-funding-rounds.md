---
name: Screen recent funding rounds with Crunchbase Search
description: Build a structured, repeatable Crunchbase search over funding rounds — resolving every identifier-valued filter first so the query cannot silently return zero rows.
api: openapi/crunchbase-data-core-financials-openapi.yml
operations:
  - autocompletes
  - searchFundingRounds
  - getFundingRound
  - getOrganization
generated: '2026-08-14'
method: generated
source: >-
  Grounded in operationIds verified present in openapi/crunchbase-data-*-openapi.yml,
  plus conventions/crunchbase-data-conventions.yml.
---

# Screen recent funding rounds with Crunchbase Search

`POST /data/searches/{collection}` is the Data API's query language. It is a JSON body
of predicates combined with AND, paged with keyset cursors. It is also where agents
most often produce a confidently wrong answer, because **an unresolved filter value is
not an error — it just matches nothing.**

## Step 1 — resolve every identifier-valued filter value first

Location and category fields take **permalinks**, not display names.
`"united-states"` matches; `"United States"` returns zero rows and no error.

`autocompletes` — `GET /data/autocompletes`

- locations: `collection_ids=locations`
- categories: `collection_ids=categories`

Do this once per filter value and cache the permalink.

## Step 2 — run the search

`searchFundingRounds` — `POST /data/searches/funding_rounds`

```json
{
  "field_ids": [
    "identifier", "announced_on", "investment_type", "money_raised",
    "funded_organization_identifier", "investor_identifiers",
    "lead_investor_identifiers", "num_investors"
  ],
  "query": [
    {"type": "predicate", "field_id": "announced_on", "operator_id": "gte", "values": ["2026-06-01"]},
    {"type": "predicate", "field_id": "investment_type", "operator_id": "includes", "values": ["seed", "series_a"]},
    {"type": "predicate", "field_id": "funded_organization_location", "operator_id": "includes", "values": ["united-states"]}
  ],
  "order": [{"field_id": "announced_on", "sort": "desc"}],
  "limit": 50
}
```

Rules that hold across every collection:

- **Money is a plain integer in USD.** `15000000`, never `"$15M"`.
- **Dates are ISO 8601.** `"2026-06-01"`.
- `limit` defaults to 50 and caps at **1000**, but the real ceiling depends on your
  licence.
- Sort fields must be sortable; the spec's per-entity `FieldId` enum is the
  authoritative list of what exists, and the field metadata says what is sortable.

## Step 3 — page the result set

Keyset only. Set `after_id` to the `uuid` of the last entity in the previous page and
re-POST the identical body. Do not attempt offset paging — there is no `offset`
parameter, and re-running without a cursor will re-return the same page.

`count` in the response is the total match count, not the page size. Use it to decide
whether paging is worth the quota.

## Step 4 — deepen only what survives screening

Screen wide and shallow with `searchFundingRounds`, then go deep on the handful that
matter:

- `getFundingRound` — `GET /data/entities/funding_rounds/{entity_id}` for the round,
  with the `investors`, `lead_investors`, `partners` or `press_references` cards.
- `getOrganization` — `GET /data/entities/organizations/{entity_id}` for the company
  behind `funded_organization_identifier`.

Never loop `getOrganization` over an unfiltered search result. It is the most
expensive call in the API and you have 200 requests per minute for everything.

## When a search returns zero rows

Loosen **one filter at a time, starting with the identifier-valued ones**. In order of
likelihood:

1. a location or category passed as a display name instead of a permalink
2. an `operator_id` the field does not accept
3. a date or money value in the wrong format
4. the filter genuinely matching nothing

A rejected search returns a `400` describing exactly what is wrong. Read it and fix
the named problem — do not fall back to a vaguer query.
