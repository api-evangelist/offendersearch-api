---
name: offendersearch-bulk-screening
description: >-
  Screen a roster of people at volume — batch (row in, row out) or asynchronous submit-and-
  collect with a signed webhook and idempotent retries.
api: Offendersearch API
base_url: https://api.offendersearch.app
operations:
  - batchSearch
  - asyncSearch
  - getSearch
generated: '2026-08-18'
method: generated
source: >-
  https://offendersearch.app/docs/batch.md and /docs/async-and-webhooks.md, grounded in
  operationIds verified in openapi/offendersearch-api-openapi.yml
---

# Bulk roster screening

Two shapes, and they solve different problems.

## Choose the shape

- **`batchSearch` — `POST /v1/batch`.** Up to **1,000** lookups in one call, JSON or CSV, one
  row in and one row out, with per-row fault isolation. Exceeding 1,000 rows returns `413`.
  **Each row bills as its own search** — a 1,000-row batch is 1,000 billable searches.
- **`asyncSearch` — `POST /v1/searches`.** One search with no request-timeout ceiling, so every
  named jurisdiction runs to completion. Right for a broad national sweep where a fast answer
  matters less than a whole one.

## Batch steps

1. `POST /v1/batch` with `X-API-Key`, either a JSON envelope whose batch-wide options apply to
   every row, or a CSV upload whose header row names `Query` fields
   (`firstName,lastName,state,dob`).
2. Read each row's own result and its own completeness fields. A failed row does not fail the
   batch.
3. `freshness` applies **per search**, so each row bills at its own tier.

## Async steps

1. `POST /v1/searches` with the same body `syncSearch` accepts, plus an optional `webhookUrl`.
2. **Always send an `Idempotency-Key` header.** A repeated key returns the original job instead
   of starting — and billing — a second search. Reuse the key for a retry of the same logical
   request; generate a fresh one for a genuinely new search.
3. Take `searchId` and `resultsUrl` from the `202`.
4. Collect the result either way:
   - **Poll** `getSearch` — `GET /v1/searches/{searchId}` — every few seconds until `status` is
     `complete` or `error`. `records` fills in as jurisdictions report.
   - **Webhook** — the finished `SearchResponse` is POSTed to your `webhookUrl` as
     `event: "search.completed"`.
5. On each result, apply the completeness contract exactly as in the nationwide-search skill:
   gate on `counts.sourcesIncomplete`, never on the record count alone.

## Verifying a webhook

Compute an HMAC-SHA256 over the **raw request body, before JSON parsing**, using your signing
secret, and compare it in constant time against the `X-Offendersearch-Signature` header. Reject
on mismatch. Delivery is **at-least-once** — de-duplicate on `searchId`. Acknowledge with a
prompt `2xx`; a non-2xx is retried with exponential backoff.

## Do not

- Do not fan out thousands of synchronous `POST /v1/search` calls; use batch or async.
- Do not retry a submission without an `Idempotency-Key` — you will be billed twice.
- Do not trust an unsigned or unverified webhook body.
