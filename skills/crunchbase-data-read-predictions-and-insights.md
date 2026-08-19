---
name: Read Crunchbase predictions and insights safely
description: Pull Crunchbase's AI-generated forecasts (funding, growth, acquisition, IPO, layoff, closure) and market insights, and present them with the provenance and package caveats they require.
api: openapi/crunchbase-data-predictions-insights-openapi.yml
operations:
  - searchFundingPredictions
  - getFundingPrediction
  - searchGrowthPredictions
  - getGrowthPrediction
  - searchAcquisitionPredictions
  - searchIpoPredictions
  - searchLayoffPredictions
  - searchClosurePredictions
  - searchInvestorMatches
  - searchMarketInsights
  - getMarketInsight
  - getMarketInsightCard
  - getOrganization
generated: '2026-08-14'
method: generated
source: >-
  Grounded in operationIds verified present in
  openapi/crunchbase-data-predictions-insights-openapi.yml, plus
  https://data.crunchbase.com/docs/predictions and
  https://data.crunchbase.com/docs/insights.
---

# Read Crunchbase predictions and insights safely

Crunchbase's Predictions and Insights entities are **model output, not observed fact**.
They forecast funding rounds, growth, acquisitions, IPOs, layoffs and closures, and
they classify markets as growing or declining. Handled carelessly, an agent will
present a probability as an event.

Three rules govern this flow: check the package first, screen before you deepen, and
never restate a prediction as a fact.

## Step 0 — confirm your package actually has them

These entities exist only in the wider packages. The six published documents differ:

| Package | Operations |
|---|---|
| `firmographic` | 43 |
| `core-financials` | 46 |
| `advanced-financials` | 57 |
| `predictions` | 71 |
| `insights` | 95 |
| `predictions-insights` | 109 |

A key licensed to `firmographic` calling `searchGrowthPredictions` gets
`[{"status":401,"code":"LA401","message":"Unauthorized user_key"}]` — a licence
failure that looks exactly like a bad key. Check the package before you debug the key.

## Step 1 — screen with search, not with per-company lookups

`POST /data/searches/{collection}` on the prediction collection you want:

- `searchFundingPredictions` — likely to raise
- `searchGrowthPredictions` — growth trajectory
- `searchAcquisitionPredictions` — likely to be acquired
- `searchIpoPredictions` — likely to go public
- `searchLayoffPredictions` — likely to cut staff
- `searchClosurePredictions` — likely to shut down
- `searchRemainPrivatePredictions` — likely to stay private

Same body shape as any other search: `field_ids`, `query` predicates combined with AND,
`order`, `limit` (default 50, max 1000), `after_id` for keyset paging. Resolve any
location or category filter value to a permalink with `autocompletes` first, or the
search silently returns nothing.

As of March 2026 Crunchbase adds **time horizons** to the acquisition, IPO and closure
predictions (0–6, 6–12, 12–24 and 24+ months). Request and surface the horizon — a
prediction without its window is not actionable.

## Step 2 — deepen selectively

Pull the individual record with `getFundingPrediction`, `getGrowthPrediction`,
`getAcquisitionPrediction`, `getIpoPrediction`, `getLayoffPrediction`,
`getClosurePrediction` or `getRemainPrivatePrediction` at
`GET /data/entities/{collection}/{entity_id}`.

Then join back to the company with `getOrganization`. Do not do this for the whole
result set — screen wide, deepen narrow, and remember the 200 requests-per-minute
budget covers everything you are doing.

## Step 3 — market insights

`searchMarketInsights` / `getMarketInsight` classify industries and micro-industries as
growing or declining, refreshed weekly. `getMarketInsightCard` with
`card_id=market_insight_reasons` returns the reasons behind the classification.

Market insights also hang off `categories`, `category_groups` and `micro_categories`
via their `market_insights` card, so you can enter the graph from either side.

Where a prediction has an explanatory entity, fetch it. A prediction with its reasons
is a finding; a prediction without them is a number.

## Step 4 — present with provenance

- Say it is a Crunchbase prediction, and give the time horizon where one exists.
- Give the confidence or score field the entity carries; do not round it into a
  binary claim.
- Never write "Acme will be acquired". Write "Crunchbase's acquisition prediction for
  Acme is X in a 6–12 month horizon."
- Crunchbase's licence requires a visible, crawlable link to the entity's Crunchbase
  page next to any data you surface. That applies to predictions too.

## Related

Funding predictions pair with `searchInvestorMatches` / `getInvestorMatch`, which
identify likely investors for companies with a positive funding prediction — so "who
might participate" is answerable, not just "will they raise".
