# Dice Job Scraper

Extract structured data from [Dice.com](https://Dice.com) — Dice.com tech job listings with structured salary (min/max/currency), full descriptions, company data, and 8+ search filters. Incremental mode tracks new/updated/expired jobs across runs. No proxy needed — $0 per request.

**[Dice.com Job Scraper - U.S. Tech Jobs on Apify →](https://apify.com/blackfalcondata/dice-com-job-scraper)**

---

## Key features




**Search with filters** — Search by keyword and location. Filter by employment type, work setting, employer type, and more.

**Detail enrichment** — Fetch full job descriptions, salary data, employer profiles, contact information for each listing.

**Incremental mode** — Only get new or changed listings since your last run. Content hash per listing — no duplicates, no re-processing.

---

## Use cases




**Data pipeline automation**
Integrate with your ETL pipeline to collect structured listings from dice.com on a schedule. Export to CSV, JSON, or directly to your database. Use compact mode to control output size.

**Market research**
Monitor listings, track trends, and analyze market dynamics with structured, deduplicated data from dice.com.

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

---

## Related products by Black Falcon Data




- [StepStone Scraper](https://github.com/BlackFalconData-org/stepstone-scraper) — Job listings from 18 European portals
- [Indeed Job Scraper](https://github.com/BlackFalconData-org/indeed-job-scraper) — Indeed job listings with salary data
- [Glassdoor Job Scraper](https://github.com/BlackFalconData-org/glassdoor-job-scraper) — Glassdoor listings with company ratings

---

*Last updated: 2026 03*
