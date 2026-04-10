---
name: firecrawl-build-search
description: Integrate Firecrawl `/search` into product code and agent workflows. Use when an app needs discovery before extraction, when the feature starts with a query instead of a URL, or when the system should search the web and optionally hydrate result content.
license: ISC
metadata:
  author: firecrawl
  version: "0.1.0"
  homepage: https://www.firecrawl.dev
  source: https://github.com/firecrawl/skills
inputs:
  - name: FIRECRAWL_API_KEY
    description: Firecrawl API key for hosted Firecrawl requests.
    required: true
  - name: FIRECRAWL_API_URL
    description: Optional base URL for self-hosted Firecrawl deployments.
    required: false
---

# Firecrawl Build Search

Use this when the application starts with a query, not a URL.

## Use This When

- the user asks a question and the product must discover sources first
- the feature needs current web results
- you want to turn a search query into a shortlist of pages for later scraping

## Default Recommendations

- Use `/search` first when URL discovery is part of the product behavior.
- Keep search and extraction conceptually separate unless scraping search results is clearly required.
- Prefer selective follow-up extraction over broad hydration when cost or latency matters.

## Common Product Patterns

- answer generation with cited sources
- company, competitor, or topic discovery
- research workflows that produce a shortlist before deeper extraction
- query-to-URL pipelines for later `/scrape` or `/interact`

## Escalation Rules

- If you already have the URL, use [firecrawl-build-scrape](../firecrawl-build-scrape/SKILL.md).
- If the result page then requires clicks or form interaction, escalate to [firecrawl-build-interact](../firecrawl-build-interact/SKILL.md).
- If the search target is a known site and you only need URLs on that site, [firecrawl-build-map](../firecrawl-build-map/SKILL.md) may be a better fit.

## Implementation Notes

- Treat `/search` as discovery, ranking, and source selection.
- Be explicit about whether the product needs snippets, URLs, or full result content.
- Keep the query contract stable so downstream scraping logic stays predictable.

## Docs (Source of Truth)

Read the docs for request/response schemas, parameters, and SDK examples before writing integration code:

- [docs.firecrawl.dev/features/search](https://docs.firecrawl.dev/features/search)

## See Also

- [firecrawl-build](../firecrawl-build/SKILL.md)
- [firecrawl-build-scrape](../firecrawl-build-scrape/SKILL.md)
- [firecrawl-build-map](../firecrawl-build-map/SKILL.md)
