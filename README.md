# HealthData.gov

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
