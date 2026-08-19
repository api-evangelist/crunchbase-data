---
name: Resolve and enrich a company with Crunchbase
description: Turn a company name or website domain into a Crunchbase entity identifier, then pull the firmographic and funding profile for it without burning quota.
api: openapi/crunchbase-data-firmographic-openapi.yml
operations:
  - autocompletes
  - getOrganization
  - getOrganizationCard
generated: '2026-08-14'
method: generated
source: >-
  Grounded in operationIds verified present in openapi/crunchbase-data-*-openapi.yml,
  plus conventions/crunchbase-data-conventions.yml and
  errors/crunchbase-data-problem-types.yml.
---

# Resolve and enrich a company with Crunchbase

The Crunchbase Data API never takes a display name. Every call operates on an
**identifier** — a UUID or a permalink. Skipping the resolve step is the single most
common way to get an empty result that looks like a valid answer.

## Before you start

- Base URL is `https://api.crunchbase.com/v4` and every path in the spec starts with
  `/data/`, so real requests go to `https://api.crunchbase.com/v4/data/...`.
- Send the key as the `X-cb-user-key` header. The `user_key` query parameter also
  works but puts a long-lived credential in URLs and logs.
- HTTPS only. Plain HTTP returns **426**, not a redirect.
- Stay under **200 requests per minute**. There are no `RateLimit-*` or `Retry-After`
  headers, so budget client-side; on **429** back off exponentially with jitter.
- An unlicensed or wrong-package key returns
  `[{"status":401,"code":"LA401","message":"Unauthorized user_key"}]` — a JSON array,
  not the object the spec's `Errors` schema describes.

## Step 1 — resolve the name to an identifier

`autocompletes` — `GET /data/autocompletes`

| Parameter | Value |
|---|---|
| `query` | the company name as the user gave it |
| `collection_ids` | `organizations` |
| `limit` | 10 (max 25) |

Read `entities[].identifier` from the response. Keep both `uuid` and `permalink`;
`permalink` is what filter values want later.

**Do not guess a permalink from the domain.** `acme.com` is not reliably
`acme`. If autocomplete returns several plausible matches, present them rather than
picking one — Crunchbase carries many same-named entities.

## Step 2 — pull the profile

`getOrganization` — `GET /data/entities/organizations/{entity_id}`

Pass the `uuid` or `permalink` from step 1 as `entity_id`.

- `field_ids` — name the fields you want. The organization entity has **103** fields;
  the default set is not free. Start with
  `identifier,short_description,categories,location_identifiers,founded_on,company_type,num_employees_enum,funding_total,last_funding_type,last_funding_at,funding_stage,website,linkedin`.
- `card_ids` — name the relationships you want. Organizations expose **41** cards.
  Each card returned inline is capped at **100 items**.

Useful cards for an enrichment pass: `raised_funding_rounds`, `investors`,
`founders`, `headquarters_address`, `parent_organization`, `similar_organizations`.

## Step 3 — page a card that is bigger than 100

`getOrganizationCard` — `GET /data/entities/organizations/{entity_id}/cards/{card_id}`

Only reach for this when the inline card hit the 100-item cap. Page with keyset
cursors: set `after_id` to the `identifier.uuid` of the last item you received, and
`limit` to the page size you want. There is no `next` link and no opaque page token —
the cursor is the last UUID.

## Failure modes

| Symptom | Cause | Fix |
|---|---|---|
| `404` on `getOrganization` | the identifier does not exist in `organizations` | re-resolve with `autocompletes`; check the entity is not a person or a fund |
| `401` `LA401` | key missing, invalid, or licensed to a narrower package | confirm the operation is in the package your key holds — `firmographic` exposes 43 operations, `predictions-insights` exposes 109 |
| Card looks truncated | inline cards cap at 100 | switch to `getOrganizationCard` with `after_id` |
| `400` | malformed request | check `field_ids`/`card_ids` are valid enum members for this entity |

## Attribution

Crunchbase's licence requires that any surfaced data carry a visible, crawlable
hyperlink (no `nofollow`) to the relevant Crunchbase entity page, placed close to the
data. If you render the result, render the link.
