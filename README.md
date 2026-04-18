# Dice Job Scraper

Extract structured data from [Dice.com](https://Dice.com) — Dice.com tech job listings with structured salary (min/max/currency), full descriptions, company data, and 8+ search filters. Incremental mode tracks new/updated/expired jobs across runs. No proxy needed — $0 per request.

**[Dice.com Job Scraper - U.S. Tech Jobs on Apify →](https://apify.com/blackfalcondata/dice-com-job-scraper?fpr=1h3gvi)**

---

## Key features





**Search with filters** — Search by keyword and location. Filter by employment type, work setting, employer type, and more.

**Detail enrichment** — Fetch full job descriptions, salary data, employer profiles, contact information for each listing.

**Incremental mode** — Only get new or changed listings since your last run. Content hash per listing — no duplicates, no re-processing.

**Change classification** — Track unchanged, expired, cross-run repost detection across runs. Build audit trails of how listings evolve over time.

**Compact output** — Emit core fields only (AI-agent / MCP-friendly). Keeps response size small for LLM workflows.

**Description truncation** — Cap description length per listing to control output size and cost.

**Result cap** — Stop after N listings (up to 1.000). Set to 0 for the full catalog.

**Export anywhere** — Download as JSON, CSV, or Excel. Stream via Apify API, webhooks, or integrations with Make, Zapier, Airbyte, Keboola.

**Structured data** — Every listing returns the same schema with consistent field naming. All fields always present — `null` when unavailable, never omitted.

---

## Use cases





**Data pipeline automation**
Integrate with your ETL pipeline to collect structured listings from dice.com on a schedule. Export to CSV, JSON, or directly to your database. Use compact mode to control output size.

**Market research**
Monitor listings, track trends, and analyze market dynamics with structured, deduplicated data from dice.com.

**Change monitoring**
Run daily or hourly in incremental mode to capture only new, updated, or expired listings. Perfect for price-tracking, churn analysis, and alerting pipelines.

**Compensation benchmarking**
Aggregate salary ranges across roles, industries, and locations on dice.com to inform pricing decisions, hiring plans, or candidate negotiations.

**AI / LLM training data**
Structured JSON per listing is ready for RAG pipelines, embeddings, and agent workflows. Compact mode trims tokens for LLM context windows.

---

## Quick start

```json
{
  "query": "software engineer",
  "maxResults": 50,
  "includeDetails": true
}
```

---

## Input parameters

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `query` | string | — | Job search keywords. Use JSON array for multi-query, e.g. ["python", "java"]. |
| `location` | string | — | City, state, or region. Use JSON array for multi-location, e.g. ["New York", "San Francisco"]. |
| `radius` | integer | — | Distance radius from location in miles. Common values: 10, 25, 50, 75, 100. |
| `employmentType` | enum | — | Filter by employment type. |
| `remoteFilter` | enum | — | Filter by workplace type. |
| `employerType` | enum | — | Filter by employer type. |
| `easyApply` | boolean | `false` | Only return jobs that support Easy Apply. |
| `postedDate` | enum | — | Only return jobs posted within this time period. |
| `startUrls` | array | — | Direct Dice search or job detail URLs. Overrides query/location. |
| `maxResults` | integer | `50` | Maximum total job listings to return. 0 = unlimited. |
| `maxPages` | integer | `5` | Maximum SERP pages to scrape per search source. |
| `includeDetails` | boolean | `true` | Fetch each job's detail page for full description, structured salary, and contact info. |
| `includeCompanyProfile` | boolean | `false` | Fetch company overview pages for industry, headcount, and more. |
| `descriptionMaxLength` | integer | `0` | Truncate description to this many characters. 0 = no truncation. |
| `compact` | boolean | `false` | Output only core fields — optimized for AI-agent and MCP workflows. |
| `incrementalMode` | boolean | `false` | Track changes across runs. Only emit NEW, UPDATED, and optionally EXPIRED jobs. Requires stateKey. |
| `stateKey` | string | — | Stable identifier for the tracked search universe (e.g. "us-software-nyc"). Required when incrementalMode is true. |
| `emitUnchanged` | boolean | `false` | When incremental, also emit records that haven't changed since last run. |
| `emitExpired` | boolean | `false` | When incremental, also emit records no longer found in search results. |

---

## FAQ

**How to scrape dice?**
Use this actor on Apify to extract structured job listings from Dice.com. Set your search query and filters in the input, then run — no coding needed.

**Is there a dice API?**
Dice.com does not offer a structured data export. This actor works as an unofficial API, returning structured JSON data from dice.

**Is it legal to scrape Dice.com?**
Web scraping of publicly available data is generally legal. This actor only accesses publicly visible information. Always check the target site's terms of service for your specific use case.

**How does incremental mode work?**
Each listing gets a content hash. On subsequent runs, only new or changed listings are emitted — saving time, compute, and storage.

---

## Known limitations

<!-- WRITE: 4-6 honest limitations -->

- <!-- WRITE: limitation 1 -->
- <!-- WRITE: limitation 2 -->


## Output fields

Every listing returns the same 47-field schema. Missing values are `null` — never omitted.

- `jobId`
- `jobKey`
- `title`
- `company`
- `companyUrl`
- `companyProfileId`
- `companyLogoUrl`
- `location`
- `postalCode`
- `applicantLocationRequirements`
- `description`
- `descriptionHtml`
- `descriptionLength`
- `salaryText`
- `salaryMin`
- `salaryMax`
- `salaryCurrency`
- `salaryType`
- `employmentType`
- `workplaceTypes`
- `employerType`
- `skills`
- `easyApply`
- `postedDate`
- `modifiedDate`
- `validThrough`
- `canonicalUrl`
- `applyUrl`
- `portalUrl`
- `sourceUrl`
- `sourceCountry`
- `sourceDomain`
- `searchQuery`
- `searchUrl`
- `isSponsored`
- `fetchedAt`
- `scrapedAt`
- `detailFetched`
- `contentQuality`
- `extractedEmails`
- `contactName`
- `diceJobId`
- `positionId`
- `companyIndustry`
- `companyEmployeeRange`
- `companyWebsite`
- `companyDescription`


## Sample output

One object per listing. Here is a real example from a production run:

```json
{
  "jobId": "09be02b4589309e355b2d783a450d18ea8a09622ee6ca6ae1dcceda4180f2895",
  "jobKey": "5cf13c8d-bea1-4ff8-b734-99681e3b69eb",
  "title": "Sr Software Engineer",
  "company": "Randstad Digital",
  "companyUrl": null,
  "companyProfileId": "ee3855f3-d056-5325-bc31-ad5f53052a28",
  "companyLogoUrl": "https://d3qscgr6xsioh.cloudfront.net/nwd2B9CDT8Oo4K91VMeJ_transformed.png?format=webp",
  "location": "Jersey City, New Jersey, USA",
  "postalCode": "07310",
  "applicantLocationRequirements": "USA",
  "description": "job summary:Proficient in working with Oracle/CrDB, creating & leading database objects like tables, views, indexes, Stored Procs and optimizing database performance through query …",
  "descriptionHtml": "job summary:<br><br><p>Proficient in working with Oracle/CrDB, creating &amp; leading database objects like tables, views, indexes, Stored Procs and optimizing database performance…"
}
```

*Truncated — full records contain 47 fields. See Output fields for the complete schema.*


**[Try Dice.com Job Scraper - U.S. Tech Jobs now — $5 free credit, no credit card →](https://apify.com/blackfalcondata/dice-com-job-scraper?fpr=1h3gvi)**


## Pricing

Pay only for what you extract. No subscription required — Apify's free $5 credit covers thousands of results.

| Event | Price (USD) |
| --- | --- |
| Actor Start | $0.01 |
| Result | $0.002 |

See the [actor on Apify](https://apify.com/blackfalcondata/dice-com-job-scraper?fpr=1h3gvi) for current pricing.

---

## Related products by Black Falcon Data





- [StepStone Scraper](https://apify.com/blackfalcondata/stepstone-scraper?fpr=1h3gvi) — Job listings from 18 European portals
- [Indeed Job Scraper](https://apify.com/blackfalcondata/indeed-job-scraper?fpr=1h3gvi) — Indeed job listings with salary data
- [Glassdoor Job Scraper](https://apify.com/blackfalcondata/glassdoor-job-scraper?fpr=1h3gvi) — Glassdoor listings with company ratings
- [Arbeitsagentur Scraper](https://apify.com/blackfalcondata/arbeitsagentur-scraper?fpr=1h3gvi) — Germany's official job portal (1M+ listings)
- [SEEK Scraper](https://apify.com/blackfalcondata/seek-scraper?fpr=1h3gvi) — Australia & NZ's largest job board
- [Naukri Scraper](https://apify.com/blackfalcondata/naukri-scraper?fpr=1h3gvi) — India's largest job portal


## Getting started with Apify

New to Apify? [Create a free account with $5 credit](https://console.apify.com/sign-up?fpr=1h3gvi) — no credit card required.

1. [Sign up free](https://console.apify.com/sign-up?fpr=1h3gvi) — $5 credit included
2. Open the actor and paste your input
3. Click Start — results download as JSON, CSV, or Excel

Need more volume? [See pricing](https://apify.com/pricing?fpr=1h3gvi).

---


## About Black Falcon Data

Black Falcon Data builds production-grade web scrapers for job boards and marketplace data. Browse our full actor catalog at [www.blackfalcondata.com](https://www.blackfalcondata.com).

---
---

*Last updated: 2026 03*
