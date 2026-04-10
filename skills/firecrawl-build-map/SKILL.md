---
name: firecrawl-build-map
description: Integrate Firecrawl `/map` into product code for URL discovery on a known site. Use when a feature needs to find pages before scraping or crawling, especially on large docs sites, blogs, or help centers where the exact target URLs are not known yet.
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

# Firecrawl Build Map

Use this when the product knows the site but not the exact URLs.

## Use This When

- the feature starts with a domain or site section
- you need URL discovery before extraction
- the product should inspect site structure without doing a full crawl yet

## Guidance

- Use `/map` before `/crawl` when URL discovery itself is the main job.
- Combine `/map` with `/scrape` when you only need a filtered subset of pages.
- Keep this as lighter coverage than `/scrape`, `/search`, and `/interact` unless the feature is navigation-heavy.

## When Not To Use It

- If you already have the exact URL, use [firecrawl-build-scrape](../firecrawl-build-scrape/SKILL.md).
- If the feature begins with a general query across the web, use [firecrawl-build-search](../firecrawl-build-search/SKILL.md).

## Docs (Source of Truth)

Read the docs for request/response schemas, parameters, and SDK examples before writing integration code:

- [docs.firecrawl.dev/features/map](https://docs.firecrawl.dev/features/map)

## See Also

- [firecrawl-build](../firecrawl-build/SKILL.md)
- [firecrawl-build-search](../firecrawl-build-search/SKILL.md)
- [firecrawl-build-crawl](../firecrawl-build-crawl/SKILL.md)
