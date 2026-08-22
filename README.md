# HealthData.gov

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

HealthData.gov is the U.S. Department of Health and Human Services open data platform providing public access to federal health datasets. The platform hosts data from CMS, CDC, FDA, NIH, and other HHS agencies, covering Medicare claims, hospital quality ratings, drug utilization, public health indicators, and thousands of additional health-related datasets.

## API Access

Every dataset on HealthData.gov is accessible via the **Socrata Open Data API (SODA)**. Endpoints follow a consistent pattern using an eight-character dataset identifier:

```
https://healthdata.gov/api/views/{dataset-id}/rows.json
https://healthdata.gov/api/v3/views/{dataset-id}/query.json
```

Queries are written in **SoQL (Socrata Query Language)**, a SQL-like syntax supporting `SELECT`, `WHERE`, `ORDER BY`, `GROUP BY`, `LIMIT`, and `OFFSET` clauses.

### Example: State Drug Utilization Data

```
GET https://healthdata.gov/resource/itpq-ryxs.json?$limit=100&$where=year=2024
```

## Authentication

- **No auth required** for all public datasets
- **App Token** (free, recommended): Include `X-App-Token: YOUR_TOKEN` header to avoid IP-based throttling
- **OAuth 2.0**: Required only for write access to permissioned datasets

Register a free app token at: https://dev.socrata.com/docs/app-tokens.html

## Rate Limits

| Tier | Limit |
|------|-------|
| Anonymous (no token) | Shared IP pool, no published number |
| App Token (free) | ~1,000 requests/hour (guideline); not actively throttled for legitimate use |
| Elevated (by request) | Custom, contact Socrata support |

Max rows per response: **50,000** (paginate with `$limit` / `$offset`)

## Pricing

All access is **free**. HealthData.gov is a U.S. federal government open data initiative funded by congressional appropriations.

## Key Datasets

- Hospital Compare / Care Compare quality data
- Medicare Inpatient and Outpatient charge data
- State Drug Utilization Data (Medicaid)
- Community Health Indicators
- CDC WONDER public health statistics
- ClinicalTrials.gov registry data
- RxNorm / RxNav drug information APIs

## Links

- Portal: https://healthdata.gov
- Data Catalog: https://healthdata.gov/browse
- SODA Developer Docs: https://dev.socrata.com/consumers/getting-started.html
- GitHub (HHS): https://github.com/HHS/healthdata.gov
- HHS Developer Center: https://www.hhs.gov/web/developer/index.html
- HHS Open Data Plan: https://cdo.hhs.gov/s/open-data

## APIs.json

This repository contains an [APIs.json 0.19](https://apisjson.org) profile for HealthData.gov:

- `apis.yml` — primary catalog index
- `plans/plans.yml` — access tier descriptions
- `rate-limits/rate-limits.yml` — throttling policies
- `finops/finops.yml` — cost and budget guidance
