---
name: Keep a local Crunchbase mirror reconciled
description: Use the deleted-entities delta feed to remove records that have left the Crunchbase Graph, so a downstream database does not keep serving entities Crunchbase has retracted.
api: openapi/crunchbase-data-firmographic-openapi.yml
operations:
  - getDeletedEntities
  - getDeletedEntitiesForCollection
  - getOrganization
generated: '2026-08-14'
method: generated
source: >-
  Grounded in operationIds verified present in openapi/crunchbase-data-*-openapi.yml,
  plus https://data.crunchbase.com/docs/using-deleted-entities-api.
---

# Keep a local Crunchbase mirror reconciled

Entities leave the Crunchbase Graph — for compliance, data-quality cleanup, or
inappropriate content. A search or lookup will simply stop returning them, which means
a mirror that only ever adds rows will keep serving records Crunchbase has retracted.
The deleted-entities feed is the only way to learn about a deletion.

This is also the one capability with **no MCP equivalent**. An agent working purely
through `mcp.crunchbase.com` cannot see deletions at all; this flow is REST-only.

## Step 1 — pull the delta

`getDeletedEntities` — `GET /data/deleted_entities`

| Parameter | Value |
|---|---|
| `collection_ids` | comma-separated collections to scope to, e.g. `organizations,people,funding_rounds` |
| `deleted_at_order` | `asc` to walk forward from your last sync, `desc` to see newest first |
| `limit` | page size |
| `after_id` | keyset cursor — the `uuid` of the last record from the previous page |

Scope to one collection with
`getDeletedEntitiesForCollection` — `GET /data/deleted_entities/{collection_id}` — when
you only mirror one entity type.

Each record carries `uuid`, `deleted_at` and `entity_def_id`.

## Step 2 — walk the whole delta, in order

Sort `asc` and page with `after_id` until the page comes back short. Persist the
`deleted_at` of the last record you processed as your watermark — **not** the wall-clock
time of the run, or a slow page will silently skip deletions.

## Step 3 — apply, do not guess

For each returned `uuid`, tombstone the matching record in your store. Use
`entity_def_id` to route to the right table; the same UUID space spans all collections.

Do **not** try to confirm a deletion by calling `getOrganization` on the UUID. A 404
there is ambiguous — it can also mean the entity is outside your licensed package. The
delta feed is the authoritative signal.

## Cadence and cost

- Run on a schedule matched to how stale your mirror may be, not continuously — the
  200 requests-per-minute budget is shared with everything else you do.
- The feed is unbounded backwards. On a first run, take the newest page and set your
  watermark from it rather than trying to replay all history.

## Failure modes

| Symptom | Cause | Fix |
|---|---|---|
| Same page repeats | `after_id` not advanced | set `after_id` to the `uuid` of the **last** record in the page you just processed |
| Deletions appear to skip | watermark taken from clock time | watermark on the last processed `deleted_at` instead |
| `401` `LA401` | key not licensed for the collection | the deleted-entities endpoints exist in every package, but the collections you can scope to follow your licence |
