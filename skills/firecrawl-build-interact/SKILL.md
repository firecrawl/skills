---
name: firecrawl-build-interact
description: Integrate Firecrawl `/interact` into product code for dynamic pages and browser actions after scraping. Use when a feature needs clicks, form fills, pagination, authentication-aware flows, or other multi-step interactions that plain `/scrape` cannot complete.
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

# Firecrawl Build Interact

Use this when `/scrape` is not enough because the feature needs to act on the page.

## Use This When

- content appears only after clicks, typing, or navigation
- the feature needs forms, pagination, filters, or multi-step flows
- the product must stay in the same browser context after scraping

## Default Recommendations

- Start with `/scrape`, then escalate to `/interact`.
- Keep `/interact` scoped to the smallest browser workflow that unlocks the data.
- Use persistent profiles only when the feature truly needs authenticated state across sessions.

## Common Product Patterns

- search forms and faceted filters
- paginated result sets
- login-gated dashboards or tools
- flows where the page must be explored before extraction is complete

## Implementation Notes

- `/interact` is the right tool when the page must be manipulated, not just read.
- Keep prompts or action code specific to the product flow.
- If the use case is fully open-ended browser automation, evaluate whether a browser sandbox is a better product fit.

## Escalation Rules

- If the page can be read directly, stay on [firecrawl-build-scrape](../firecrawl-build-scrape/SKILL.md).
- If you need a site-wide or section-wide extraction job, use [firecrawl-build-crawl](../firecrawl-build-crawl/SKILL.md) instead of driving one page at a time.

## Docs (Source of Truth)

Read the docs for request/response schemas, parameters, and SDK examples before writing integration code:

- [docs.firecrawl.dev/features/interact](https://docs.firecrawl.dev/features/interact)

## See Also

- [firecrawl-build](../firecrawl-build/SKILL.md)
- [firecrawl-build-scrape](../firecrawl-build-scrape/SKILL.md)
- [firecrawl-build-search](../firecrawl-build-search/SKILL.md)
