# Integration Patterns

Firecrawl integrations usually fall into one of these shapes:

## Known URL -> extract content

Use `/scrape` when the application already has the URL.

Examples:

- documentation import from a saved URL
- pricing extraction from a competitor page
- content ingestion into a retrieval pipeline

## Query -> discover -> extract

Use `/search` when the product begins with a search query. Only scrape follow-up pages if the product needs full content.

Examples:

- answer generation with fresh sources
- competitor discovery
- research workflows that produce a shortlist of URLs

## Scrape -> interact -> extract

Use `/interact` only when the page must be manipulated after scrape.

Examples:

- click-to-reveal sections
- form-driven search results
- paginated listings
- authenticated dashboards

## Site -> discover URLs -> extract subset

Use `/map` when the site is known but target URLs are not.

Examples:

- finding the auth page in a docs site
- identifying blog post URLs before enrichment

## Site section -> bulk extraction

Use `/crawl` when the product needs many pages in one run.

Examples:

- help center ingestion
- docs sync jobs
- blog archive imports
