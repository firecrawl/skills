---
name: firecrawl
description: Integrate Firecrawl into an application, agent, or workflow. Use when adding Firecrawl to a codebase, choosing between `/scrape`, `/search`, `/interact`, `/crawl`, and `/map`, setting up `FIRECRAWL_API_KEY`, or wiring a Firecrawl SDK or REST call into product code. Do not use this skill for ad hoc web tasks during the current session; use `firecrawl/cli` for those.
license: ISC
metadata:
  author: firecrawl
  version: "0.1.0"
  homepage: https://www.firecrawl.dev
  source: https://github.com/firecrawl/skills
inputs:
  - name: FIRECRAWL_API_KEY
    description: Firecrawl API key for cloud usage. Store it in `.env` or the runtime environment before making Firecrawl API calls.
    required: true
  - name: FIRECRAWL_API_URL
    description: Optional base URL for self-hosted Firecrawl deployments. Only set this when the project is not using the hosted `api.firecrawl.dev`.
    required: false
references:
  - references/endpoint-selection.md
  - references/integration-patterns.md
  - references/sdk-installation.md
  - references/auth-and-env.md
---

# Firecrawl

Use this skill when the task is "build with Firecrawl," not "use Firecrawl as a terminal tool right now."

## Use This When

- a project needs live web data
- an agent should call Firecrawl from application code
- you need to choose the right endpoint before implementation
- you need `FIRECRAWL_API_KEY` in the project

If the task is "search the web," "scrape this page for me," or "interact with a live site during this session," install and use `firecrawl/cli` instead.

## Quick Start

Start with the narrowest endpoint that fits:

- `/scrape` for one known URL
- `/search` when you have a query instead of a URL
- `/interact` when `/scrape` must continue into clicks, forms, or navigation
- `/crawl` for many pages in the same site section
- `/map` when you know the site but not the URLs yet

## What Do You Need?

| Task                                                 | Reference                                                                |
| ---------------------------------------------------- | ------------------------------------------------------------------------ |
| **Choose the right endpoint**                        | [references/endpoint-selection.md](references/endpoint-selection.md)     |
| **Wire Firecrawl into product code**                 | [references/integration-patterns.md](references/integration-patterns.md) |
| **Install an SDK or use REST**                       | [references/sdk-installation.md](references/sdk-installation.md)         |
| **Set up `FIRECRAWL_API_KEY` or self-hosted config** | [references/auth-and-env.md](references/auth-and-env.md)                 |
| **Get credentials into the project**                 | [firecrawl-app-onboarding](../firecrawl-app-onboarding/SKILL.md)         |
| **Implement single-page extraction**                 | [firecrawl-scrape](../firecrawl-scrape/SKILL.md)                         |
| **Implement discovery-first flows**                  | [firecrawl-search](../firecrawl-search/SKILL.md)                         |
| **Implement post-scrape browser actions**            | [firecrawl-interact](../firecrawl-interact/SKILL.md)                     |
| **Implement bulk extraction**                        | [firecrawl-crawl](../firecrawl-crawl/SKILL.md)                           |
| **Implement URL discovery**                          | [firecrawl-map](../firecrawl-map/SKILL.md)                               |

## Default Integration Order

1. Get `FIRECRAWL_API_KEY` or `FIRECRAWL_API_URL` right.
2. Choose the endpoint that matches the product behavior.
3. Install the SDK for the target stack, or call REST directly.
4. Keep endpoint-specific implementation details in the narrower skills linked above.

## Boundary With The CLI

Use this repo for application integration.

Use `firecrawl/cli` for:

- one-off research during the current task
- terminal workflows and command syntax
- editor setup for live web tooling
