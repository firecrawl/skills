---
name: firecrawl-build-crawl
description: Integrate Firecrawl `/crawl` into product code for bulk extraction across a site or site section. Use when a feature needs many related pages, such as documentation sets, help centers, or blogs, and page-by-page `/scrape` would be too manual.
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

# Firecrawl Build Crawl

Use this when the product needs many pages from the same site, not just one.

## Use This When

- the feature targets a docs section, blog, or help center
- you need bulk extraction with path or depth boundaries
- the product should ingest or refresh a site section at once

## Guidance

- Keep crawl scope narrow with path, depth, or page-count constraints.
- Prefer `/crawl` over many manual `/scrape` calls when the site structure is stable.
- Treat this as secondary to `/scrape`, `/search`, and `/interact` unless the feature is clearly site-wide.

## When Not To Use It

- If you only need one known URL, use [firecrawl-build-scrape](../firecrawl-build-scrape/SKILL.md).
- If you first need to discover URLs on a single site, start with [firecrawl-build-map](../firecrawl-build-map/SKILL.md).

## Docs (Source of Truth)

Read the docs for request/response schemas, parameters, and SDK examples before writing integration code:

- [docs.firecrawl.dev/features/crawl](https://docs.firecrawl.dev/features/crawl)

## See Also

- [firecrawl-build](../firecrawl-build/SKILL.md)
- [firecrawl-build-map](../firecrawl-build-map/SKILL.md)
- [firecrawl-build-scrape](../firecrawl-build-scrape/SKILL.md)
