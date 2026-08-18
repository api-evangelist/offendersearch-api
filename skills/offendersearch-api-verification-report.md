---
name: offendersearch-verification-report
description: >-
  Produce a timestamped verification-report PDF for a search you already ran, with a source
  citation on every record, for an audit file.
api: Offendersearch API
base_url: https://api.offendersearch.app
operations:
  - syncSearch
  - makeReport
  - getProofDoc
generated: '2026-08-18'
method: generated
source: >-
  https://offendersearch.app/docs/reports.md and https://offendersearch.app/pricing, grounded
  in operationIds verified in openapi/offendersearch-api-openapi.yml
---

# Verification report

A defensible artifact for an audit file: a branded, timestamped PDF of a search, every match,
every field, and a source citation on every record.

## Steps

1. **Run the search first.** `syncSearch` — `POST /v1/search`. Keep the `searchId` off the
   response envelope.
2. **Call `makeReport`** — `POST /v1/report` — passing that `searchId`. The search must have run
   within the last **7 days**. Add the requester context that is printed onto the document:
   `viewerName`, `viewerEmail`, `requesterName`, `purpose`, `reference`.
3. **Read the response as a document.** The response is a PDF; the `X-Report-Id` response header
   identifies it. Write it to a file rather than parsing it.
4. **Re-fetch a rendered document** with `getProofDoc` — `GET /v1/proof-docs/{token}` — when you
   need the artifact again rather than a new one.

## Billing

Any valid key can call `POST /v1/report` — there is **no per-key entitlement**. The report bills
**+$0.02 per document**; the search it references was already billed, so it is not billed again.

## Not the same thing

`makeProof` — `POST /v1/searches/{searchId}/proof` — is a different, internal add-on producing
per-registry look-alike proof documents. It carries its own per-document charge and returns
`402` without billing enabled. It is **not** the customer verification report; do not substitute
one for the other.

## Do not

- Do not generate a report for a search older than 7 days — re-run the search first.
- Do not present the PDF as a consumer report or as the basis of an FCRA-governed decision.
