# Superseded modelled specs

These five documents were **modelled from the public Crunchbase documentation** during
the first profiling round (2026-07-11), when no machine-readable contract had been
found. They said so honestly in `info.x-endpoints-modeled`: paths, methods, auth and
rate limits were confirmed from `data.crunchbase.com/docs`, but field-level
request/response schemas were written from prose because live responses are
licence-gated.

They are superseded as of **2026-08-14**.

Crunchbase does publish a machine-readable contract. It is indexed by an RFC 9727
API catalog at `https://data.crunchbase.com/.well-known/api-catalog`, whose six
`service-desc` links resolve to first-party OpenAPI 3.0.1 documents at
`https://data.crunchbase.com/openapi/{advanced-financials,core-financials,firmographic,insights,predictions-insights,predictions}.yaml`.
All six were fetched (HTTP 200), verified to belong to Crunchbase
(`servers[]: https://api.crunchbase.com/v4`, `info.contact.email:
partnerships@crunchbase.com`, `info.termsOfService:
https://data.crunchbase.com/docs/terms`, security scheme `X-cb-user-key`), and saved
verbatim to `openapi/`.

The difference in coverage:

| | modelled | harvested |
|---|---|---|
| documents | 1 (+4 tag splits) | 6 (one per licence package) |
| unique operations | 6 | 109 |
| entity collections | 4 logical surfaces | 43 |
| schemas | 9 | 69–185 per document |

Nothing in this directory is referenced by `apis.yml`. It is kept only so the
provenance of the first round remains auditable — do not build artifacts from it.
