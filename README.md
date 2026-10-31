# Offendersearch API

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

Offendersearch, Inc. operates a REST API that unifies US sex-offender registry data — all 50 states, the District of Columbia, the US territories and NSOPW, 58 registries in all — behind a single authenticated endpoint. One call searches every jurisdiction and returns scored, de-duplicated records in one normalized 76-field schema, each carrying per-source provenance, a deep link back to the originating registry, and its own lastCheckedAt timestamp. Its defining contract is completeness labelling: an incomplete search is reported as partial with per-source status and a closed incompleteReason enum rather than returned as a silently empty result, so a zero from a registry that did not finish reads as UNKNOWN rather than NO MATCH. The API offers synchronous, asynchronous (with signed webhooks and Idempotency-Key retries) and 1,000-row batch/CSV modes, per-request freshness tiers, consolidated timestamped verification-report PDFs with a citation on every record, and a drop-in offenders.io compatibility endpoint. It publishes an OpenAPI 3.1 contract in JSON and YAML, an RFC 9727 api-catalog, an llms.txt, a markdown twin of every documentation page, and a documented (private-beta) MCP server. Pricing is purely metered at $0.15 per call, $0.11 above 2,000 a month. Offendersearch is expressly not a consumer reporting agency and its results are not a consumer report.

**Areas:** Background Checks · Identity Verification · Public Records · Criminal Records · Compliance · Trust and Safety · Human Resources · Recruiting · PropTech · Tenant Screening · healthcare-screening · Data API

## Offendersearch API on APIs.io

Everything profiled for Offendersearch API is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/offendersearch-api/](https://apis.io/providers/offendersearch-api/)** — or go straight to one of the APIs or properties below.

### APIs (16)

- [Offendersearch API Account API](https://apis.io/apis/offendersearch-api/offendersearch-api-account-api/) — The Account API from Offendersearch API — 1 operation(s) for account.
- [Offendersearch API Admin API](https://apis.io/apis/offendersearch-api/offendersearch-api-admin-api/) — The Admin API from Offendersearch API — 11 operation(s) for admin.
- [Offendersearch API Auth API](https://apis.io/apis/offendersearch-api/offendersearch-api-auth-api/) — The Auth API from Offendersearch API — 2 operation(s) for auth.
- [Offendersearch API Batch API](https://apis.io/apis/offendersearch-api/offendersearch-api-batch-api/) — The Batch API from Offendersearch API — 1 operation(s) for batch.
- [Offendersearch API Billing API](https://apis.io/apis/offendersearch-api/offendersearch-api-billing-api/) — The Billing API from Offendersearch API — 1 operation(s) for billing.
- [Offendersearch API Compat API](https://apis.io/apis/offendersearch-api/offendersearch-api-compat-api/) — The Compat API from Offendersearch API — 1 operation(s) for compat.
- [Offendersearch API Keys API](https://apis.io/apis/offendersearch-api/offendersearch-api-keys-api/) — The Keys API from Offendersearch API — 3 operation(s) for keys.
- [Offendersearch API Proof Docs API](https://apis.io/apis/offendersearch-api/offendersearch-api-proof-docs-api/) — The Proof Docs API from Offendersearch API — 1 operation(s) for proof docs.
- [Offendersearch API Records API](https://apis.io/apis/offendersearch-api/offendersearch-api-records-api/) — The Records API from Offendersearch API — 1 operation(s) for records.
- [Offendersearch API Report API](https://apis.io/apis/offendersearch-api/offendersearch-api-report-api/) — The Report API from Offendersearch API — 1 operation(s) for report.
- [Offendersearch API Search API](https://apis.io/apis/offendersearch-api/offendersearch-api-search-api/) — The Search API from Offendersearch API — 1 operation(s) for search.
- [Offendersearch API Searches API](https://apis.io/apis/offendersearch-api/offendersearch-api-searches-api/) — The Searches API from Offendersearch API — 3 operation(s) for searches.
- [Offendersearch API Sources API](https://apis.io/apis/offendersearch-api/offendersearch-api-sources-api/) — The Sources API from Offendersearch API — 1 operation(s) for sources.
- [Offendersearch API Support API](https://apis.io/apis/offendersearch-api/offendersearch-api-support-api/) — The Support API from Offendersearch API — 1 operation(s) for support.
- [Offendersearch API Team API](https://apis.io/apis/offendersearch-api/offendersearch-api-team-api/) — The Team API from Offendersearch API — 2 operation(s) for team.
- [Offendersearch API Usage API](https://apis.io/apis/offendersearch-api/offendersearch-api-usage-api/) — The Usage API from Offendersearch API — 1 operation(s) for usage.

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### AsyncAPI (1)

Event-driven and webhook contracts.

- [Offendersearch Api Webhooks](https://apis.io/asyncapis/offendersearch-api/offendersearch-api-webhooks/)

#### Agentic access (1)

Which operations an agent can call, which act, and which need a human in the loop.

- [Offendersearch Api Agentic Access](https://apis.io/agentic-access/offendersearch-api/offendersearch-api-agentic-access/)

#### Overlays (1)

OpenAPI overlays, including conversational phrasing for each operation.

- [Offendersearch Api Openapi Overlay](https://apis.io/overlays/offendersearch-api/offendersearch-api-openapi-overlay/)

#### Security (3)

Authentication, trust centre, and vulnerability disclosure.

- [Offendersearch Api Authentication](https://apis.io/security/offendersearch-api/offendersearch-api-authentication/)
- [Offendersearch Api Domain Security](https://apis.io/security/offendersearch-api/offendersearch-api-domain-security/)
- [Offendersearch Api Trust Center](https://apis.io/security/offendersearch-api/offendersearch-api-trust-center/)

#### Plans and pricing (1)

Published plans, tiers and prices.

- [Offendersearch Api Plans Pricing](https://apis.io/plans/offendersearch-api/offendersearch-api-plans-pricing/)

#### Rate limits (1)

Published request limits.

- [Offendersearch Api Rate Limits](https://apis.io/rate-limits/offendersearch-api/offendersearch-api-rate-limits/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://www.offendersearch.app/)
- [Pricing](https://offendersearch.app/pricing)
- [Sign up](https://offendersearch.app/sign-up)
- [Support](https://offendersearch.app/contact)
- [Blog](https://www.offendersearch.app/blog)
- [Terms of service](https://offendersearch.app/terms)
- [Privacy policy](https://offendersearch.app/privacy)

## API Evangelist rating

**Kin Score 50.1** — developing · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 75.0 |
| Contract quality | 53.9 |
| Contract governance | 4.5 |
| Operational transparency | 7.9 |
| Developer ergonomics | 58.9 |
| Access clarity | 73.7 |

**Agent readiness 44.9** — agent-native

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | derived (partial credit) |
| Reversibility Documented | — |
| MCP Server | documented (partial credit) |
| Auth Clarity | bearer (partial credit) |
| Idempotency | documented (partial credit) |
| Error Semantics | verified |
| OpenAPI Examples | partial |
| Rate Limit Signal | verified |
| Event Surface Described | yes |
| Agent Skills | derived (partial credit) |
| Well Known Catalog | yes |
| Consent Identity | — |
| Agent Card | — |
| Dry Run Mode | — |
| Delegated Identity | — |
| Protected Resource Metadata | — |
| Dynamic Client Registration | — |
| Agentic Commerce | — |
| Pagination Ratio | — |
| Operation Distinctiveness | distinct |

**Regulatory alignment 23.4** — Health

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/offendersearch-api/](https://apis.io/providers/offendersearch-api/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for Offendersearch API: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/offendersearch-api/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
