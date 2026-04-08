---
name: firecrawl-app-onboarding
description: Get Firecrawl credentials and SDK setup into a project. Use when an application needs `FIRECRAWL_API_KEY`, when an agent should add Firecrawl to `.env`, when the user wants to authenticate Firecrawl for app code, or when choosing the first SDK and docs for a new Firecrawl integration.
license: ISC
metadata:
  author: firecrawl
  version: "0.1.0"
  homepage: https://www.firecrawl.dev
  source: https://github.com/firecrawl/skills
inputs:
  - name: FIRECRAWL_API_KEY
    description: Firecrawl API key used for hosted Firecrawl API requests.
    required: true
  - name: FIRECRAWL_API_URL
    description: Optional base URL for self-hosted Firecrawl deployments.
    required: false
references:
  - references/auth-flow.md
  - references/sdk-installation.md
  - references/project-setup.md
---

# Firecrawl App Onboarding

Use this skill for the application-integration path from Firecrawl's onboarding flow.

## Use This When

- a project needs `FIRECRAWL_API_KEY`
- the user wants Firecrawl wired into `.env`
- you are adding Firecrawl to an app for the first time
- you need to choose the first SDK or REST path

Do not use this skill for CLI install flows beyond a brief pointer. That belongs to `firecrawl/cli`.

## Quick Start

If the user already has an API key, place it in `.env`:

```dotenv
FIRECRAWL_API_KEY=fc-...
```

If the project is self-hosted, also set:

```dotenv
FIRECRAWL_API_URL=https://your-firecrawl-instance.example.com
```

## What Do You Need?

| Task | Reference |
|---|---|
| **Run the browser auth flow and save `FIRECRAWL_API_KEY`** | [references/auth-flow.md](references/auth-flow.md) |
| **Install the right SDK** | [references/sdk-installation.md](references/sdk-installation.md) |
| **Put credentials into `.env` or project config** | [references/project-setup.md](references/project-setup.md) |
| **Choose the right endpoint after setup** | [firecrawl](../firecrawl/SKILL.md) |
| **Start implementation from a known URL** | [firecrawl-scrape](../firecrawl-scrape/SKILL.md) |
| **Start implementation from a query** | [firecrawl-search](../firecrawl-search/SKILL.md) |

## After Setup

Once the key is present:

1. pick the narrowest endpoint that matches the feature
2. add the SDK or REST call in code
3. use the endpoint-specific skills in this repo for implementation guidance

## See Also

- [firecrawl](../firecrawl/SKILL.md) - choose the right endpoint
- [firecrawl-scrape](../firecrawl-scrape/SKILL.md) - default starting point when you have a URL
- [firecrawl-search](../firecrawl-search/SKILL.md) - when you need discovery before extraction
