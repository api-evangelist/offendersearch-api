---
name: offendersearch-nationwide-search
description: >-
  Run one authenticated nationwide sex-offender registry search across all 58 US registries
  and read the result correctly — including the completeness contract that decides whether an
  empty result means NO MATCH or UNKNOWN.
api: Offendersearch API
base_url: https://api.offendersearch.app
operations:
  - syncSearch
generated: '2026-08-18'
method: generated
source: >-
  https://offendersearch.app/docs/search.md, /docs/result-completeness.md, /docs/errors.md,
  grounded in operationIds verified in openapi/offendersearch-api-openapi.yml
---

# Nationwide offender search

One call searches every US state, DC, the territories and NSOPW and returns scored,
de-duplicated, source-tagged records.

## Steps

1. **Authenticate.** Send `X-API-Key: <key>` on every request. Billing must be enabled on the
   account or the call returns `402`.
2. **Call `syncSearch`** — `POST /v1/search` — with a `query` object. Send at least one
   narrowing field: `lastName`, `dob`, `age`, `city`, `zipcode`, a `lat`/`lng` + `radiusMiles`
   pair, or `q`. A `firstName` alone is refused with `422`; a name + DOB query is never refused.
3. **Choose freshness deliberately.** `freshness` defaults to `daily` (freshest, +$0.01 per
   call). Send `freshness: "weekly"` for bulk or periodic re-screening at no surcharge. It
   changes how current the answer is, never which registries are searched.
4. **Read the completeness signal BEFORE the records.** This is the step that matters:
   - `status` — `complete` or `partial`.
   - `counts.sourcesQueried` / `counts.sourcesComplete` / `counts.sourcesIncomplete`.
   - `sourceStatus[].incomplete` and `sourceStatus[].incompleteReason` (a closed enum that
     says whether an identical retry can change the answer).

   **A zero from a jurisdiction that did not finish means UNKNOWN, not NO MATCH.** Never report
   "no record found" while `counts.sourcesIncomplete > 0`.
5. **Read the match quality on each record.** `matchConfidence`, `matchBasis`, `matchDetail`,
   `matchedName` and `matchState` say why a record is in the result. A partial-name or
   fuzzy search carries a confidence ceiling — do not present a low-confidence hit as an
   identification.
6. **Cite the source.** Every record carries `sources[]` with `registryName`, `recordUrl` and
   `lastCheckedAt`. Quote them; that is what makes the answer defensible.

## Paging

The full de-duplicated set comes back in one response by default. Set `query.page` and
`query.perPage` to slice it. `counts.records` is the total BEFORE the slice; compare it with
`counts.recordsReturned`. An unpaginated response is capped at 4,000 records and sets
`capped: true` — send `perPage` to reach everything.

## Errors

| Status | Do this |
|---|---|
| `401` | Fix or rotate the key sent in `X-API-Key`. |
| `402` | Billing is not enabled; add a payment method. |
| `422` | The query was DECLINED, not failed. `error.message` is written to show the user verbatim — narrow the query and resend. |
| `429` | Back off exponentially honouring `Retry-After` / `detail.retryAfterSeconds`. |
| `504` | Only when `onDeadline: "error"` was set and the deadline was hit. |

## Do not

- Do not treat a `200` as a complete answer without reading `status` and `counts`.
- Do not present results as a background check or a consumer report. Offendersearch is **not**
  a consumer reporting agency and results must not be the sole basis for an FCRA-governed
  decision.
