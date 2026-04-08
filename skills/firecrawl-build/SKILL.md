---
name: firecrawl-build
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
  - references/project-intake.md
  - references/endpoint-selection.md
  - references/integration-patterns.md
  - references/sdk-installation.md
  - references/auth-and-env.md
  - references/verification.md
---

# Firecrawl Build

Use this skill when the task is "build with Firecrawl," not "use Firecrawl as a terminal tool right now."

## Use This When

- a project needs live web data
- an agent should call Firecrawl from application code
- you need to choose the right endpoint before implementation
- you need `FIRECRAWL_API_KEY` in the project

If the task is "search the web," "scrape this page for me," or "interact with a live site during this session," install and use `firecrawl/cli` instead.

## Quick Start

First choose the project mode:

- **Fresh project** -> choose the stack, install the SDK, add env vars, and run a smoke test
- **Existing project** -> inspect the repo first, match its conventions, then integrate in place

Then ask the required question:

- **What should Firecrawl do in this product?**

Route from that answer to the narrowest endpoint that fits:

- `/scrape` for one known URL
- `/search` when you have a query instead of a URL
- `/interact` when `/scrape` must continue into clicks, forms, or navigation
- `/crawl` for many pages in the same site section
- `/map` when you know the site but not the URLs yet

## Required Intake

Always do these before writing integration code:

1. Decide whether this is a **fresh project** or an **existing project**.
2. Ask what Firecrawl should do in the product.
3. If this is an existing project, inspect the repo before choosing SDK, REST, file locations, or env handling.

For the full checklist, see [references/project-intake.md](references/project-intake.md).

## What Do You Need?

| Task | Reference |
|---|---|
| **Choose fresh project vs existing project flow** | [references/project-intake.md](references/project-intake.md) |
| **Choose the right endpoint** | [references/endpoint-selection.md](references/endpoint-selection.md) |
| **Wire Firecrawl into product code** | [references/integration-patterns.md](references/integration-patterns.md) |
| **Install an SDK or use REST** | [references/sdk-installation.md](references/sdk-installation.md) |
| **Set up `FIRECRAWL_API_KEY` or self-hosted config** | [references/auth-and-env.md](references/auth-and-env.md) |
| **Get credentials into the project** | [firecrawl-build-onboarding](../firecrawl-build-onboarding/SKILL.md) |
| **Implement single-page extraction** | [firecrawl-build-scrape](../firecrawl-build-scrape/SKILL.md) |
| **Implement discovery-first flows** | [firecrawl-build-search](../firecrawl-build-search/SKILL.md) |
| **Implement post-scrape browser actions** | [firecrawl-build-interact](../firecrawl-build-interact/SKILL.md) |
| **Implement bulk extraction** | [firecrawl-build-crawl](../firecrawl-build-crawl/SKILL.md) |
| **Implement URL discovery** | [firecrawl-build-map](../firecrawl-build-map/SKILL.md) |
| **Verify the integration actually works** | [references/verification.md](references/verification.md) |

## Default Integration Order

1. Get `FIRECRAWL_API_KEY` or `FIRECRAWL_API_URL` right.
2. Decide whether this is a fresh project or an existing codebase.
3. Ask what Firecrawl should do in the product, then choose the endpoint that matches that behavior.
4. For existing projects, inspect the repo and match its conventions before coding.
5. Install the SDK for the target stack, or call REST directly.
6. Keep endpoint-specific implementation details in the narrower skills linked above.
7. Run a smoke test that proves a real Firecrawl request succeeds.

## Boundary With The CLI

Use this repo for application integration.

Use `firecrawl/cli` for:

- one-off research during the current task
- terminal workflows and command syntax
- editor setup for live web tooling
