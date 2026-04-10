---
name: firecrawl-build-scrape
description: Integrate Firecrawl `/scrape` into product code for single-page extraction. Use when an app already has a URL and needs markdown, HTML, links, screenshots, metadata, or structured page output. Prefer this skill over broader crawl patterns when the feature is page-level.
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

# Firecrawl Build Scrape

Use this when the application already has the URL and needs content from one page.

## Use This When

- the feature starts from a known URL
- you need page content for retrieval, summarization, enrichment, or monitoring
- you want the default extraction primitive before considering `/interact`

## Default Recommendations

- Start with `/scrape`, not `/crawl`.
- Return `markdown` unless the feature truly needs another format.
- Use `onlyMainContent` for article-like pages where nav and chrome add noise.
- Add waits or other rendering options only when the page needs them.

## Common Product Patterns

- knowledge ingestion from known URLs
- enrichment from a company, product, or docs page
- pricing, changelog, and documentation extraction
- page-level quality checks or monitoring

## Escalation Rules

- If you do not have the URL yet, start with [firecrawl-build-search](../firecrawl-build-search/SKILL.md).
- If content requires clicks, typing, or multi-step navigation, escalate to [firecrawl-build-interact](../firecrawl-build-interact/SKILL.md).
- If you need many pages from the same site, consider [firecrawl-build-crawl](../firecrawl-build-crawl/SKILL.md) or [firecrawl-build-map](../firecrawl-build-map/SKILL.md).

## Implementation Notes

- Keep the integration narrow: one feature, one URL, one extraction contract.
- Treat `/scrape` as the default primitive for downstream LLM or indexing pipelines.
- Request richer formats only when the consumer needs them, such as links, screenshots, or branding data.

## Docs (Source of Truth)

Read the docs for request/response schemas, parameters, and SDK examples before writing integration code:

- [docs.firecrawl.dev/features/scrape](https://docs.firecrawl.dev/features/scrape)

## See Also

- [firecrawl-build](../firecrawl-build/SKILL.md)
- [firecrawl-build-search](../firecrawl-build-search/SKILL.md)
- [firecrawl-build-interact](../firecrawl-build-interact/SKILL.md)
