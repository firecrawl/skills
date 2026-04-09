---
name: firecrawl-build-onboarding
description: Get Firecrawl credentials and SDK setup into a project. Use when an application needs `FIRECRAWL_API_KEY`, when an agent should add Firecrawl to `.env`, when the user wants to authenticate Firecrawl for app code, or when choosing the first SDK and docs for a new Firecrawl integration. If the task is live web work during the current session, hand off to `firecrawl/cli` instead. This skill includes its own browser auth flow, so it does not depend on the website onboarding skill.
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

# Firecrawl Build Onboarding

Use this skill for the application-integration path from Firecrawl's onboarding flow.

## Use This When

- a project needs `FIRECRAWL_API_KEY`
- the user wants Firecrawl wired into `.env`
- you are adding Firecrawl to an app for the first time
- you need to choose the first SDK or REST path

If the human still needs to sign up, sign in, or authorize access in the browser, use the auth flow reference in this skill.

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

Then decide which integration path applies:

- **Fresh project** -> choose the target stack, install the SDK, add the first Firecrawl call, and run a smoke test
- **Existing project** -> inspect the repo first, then integrate Firecrawl where the project already handles third-party APIs and env vars

## What Do You Need?

| Task | Reference |
|---|---|
| **Run the browser auth flow and save `FIRECRAWL_API_KEY`** | [references/auth-flow.md](references/auth-flow.md) |
| **Install the right SDK** | [references/sdk-installation.md](references/sdk-installation.md) |
| **Put credentials into `.env` or project config** | [references/project-setup.md](references/project-setup.md) |
| **Choose the right endpoint after setup** | [firecrawl-build](../firecrawl-build/SKILL.md) |
| **Need live web tooling during this task instead** | `firecrawl/cli` |
| **Start implementation from a known URL** | [firecrawl-build-scrape](../firecrawl-build-scrape/SKILL.md) |
| **Start implementation from a query** | [firecrawl-build-search](../firecrawl-build-search/SKILL.md) |

## After Setup

Once the key is present:

1. decide whether this is a fresh project or an existing codebase
2. ask what Firecrawl should do in the product
3. pick the narrowest endpoint that matches that behavior
4. add the SDK or REST call in code
5. run a smoke test that proves one real Firecrawl request succeeds
6. use the endpoint-specific skills in this repo for implementation guidance
7. if you also need live web tooling during the current task, use `firecrawl/cli` alongside this repo
