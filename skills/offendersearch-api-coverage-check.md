---
name: offendersearch-coverage-check
description: >-
  Read the jurisdiction coverage catalog and live per-registry health — the one free,
  unauthenticated call in the API — before or alongside a search.
api: Offendersearch API
base_url: https://api.offendersearch.app
operations:
  - listSources
generated: '2026-08-18'
method: generated
source: >-
  https://offendersearch.app/docs/freshness.md, /docs/jurisdictions.md and the RFC 9727
  api-catalog, grounded in operationIds verified in openapi/offendersearch-api-openapi.yml
---

# Coverage and source-health check

## Steps

1. **Call `listSources`** — `GET /v1/sources`. It declares `security: []` in the contract: **no
   API key, no billing, no charge.** It is also the "status" link in the provider's
   `/.well-known/api-catalog`.
2. **Read each source row**: `id`, `name`, `covers[]`, `registries`, `scope`
   (`national` | state | territory), `status` (e.g. `live`), `legal.commercialUse`, and
   `health.lastSuccessAt` / `health.ageSeconds`.
3. **Respect `legal.commercialUse`.** Some jurisdictions restrict commercial use of this data.
   A search scoped exclusively to statutorily non-commercial jurisdictions is the only free
   call in the API precisely because there is nothing commercially billable in it.
4. **Scope vs filter — they are different.** `jurisdictions` selects which registries the search
   runs against; `query.state` filters the result after the fact. Use `jurisdictions` to control
   cost and latency; use `query.state` to narrow an answer.

## What this endpoint is not

`GET /v1/sources` reports **registry-source health**, not API-platform uptime. There is no
status page, no incident history and no subscribe-to-updates channel: `offendersearch.app/status`
and `status.offendersearch.app` do not exist. Do not present this as an uptime signal for
`api.offendersearch.app` itself.
