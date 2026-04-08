# Firecrawl Skills

A collection of skills for AI coding agents following the [Agent Skills](https://agentskills.io) format. Available as a plugin for Claude Code, Cursor, and OpenAI Codex.

This repo is the app-integration counterpart to [`firecrawl/cli`](https://github.com/firecrawl/cli).

- Use this repo when an agent is building a product that calls Firecrawl APIs.
- Use `firecrawl/cli` when an agent needs better web access during its own work: search the web, scrape pages, crawl docs, or interact with live sites from the terminal.

## Install

```bash
npx skills add firecrawl/skills
```

Then select the skills you want to install.

## Available Skills

| Skill                                                           | Description                                                             | Source        |
| --------------------------------------------------------------- | ----------------------------------------------------------------------- | ------------- |
| [`firecrawl-build`](./skills/firecrawl-build)                               | Firecrawl application API umbrella skill                                | Authored here |
| [`firecrawl-build-onboarding`](./skills/firecrawl-build-onboarding) | Get `FIRECRAWL_API_KEY` into a project and choose the right SDK/docs    | Authored here |
| [`firecrawl-build-scrape`](./skills/firecrawl-build-scrape)                 | Integrate `/scrape` for single-page extraction                          | Authored here |
| [`firecrawl-build-search`](./skills/firecrawl-build-search)                 | Integrate `/search` for discovery-first workflows                       | Authored here |
| [`firecrawl-build-interact`](./skills/firecrawl-build-interact)             | Integrate `/interact` for clicks, forms, and dynamic flows after scrape | Authored here |
| [`firecrawl-build-crawl`](./skills/firecrawl-build-crawl)                   | Integrate `/crawl` for bulk extraction across a site or section         | Authored here |
| [`firecrawl-build-map`](./skills/firecrawl-build-map)                       | Integrate `/map` for URL discovery on a known site                      | Authored here |

The current emphasis is on `/scrape`, `/search`, and `/interact`, with lighter coverage for `/crawl` and `/map`.

## MCP Server

The plugin includes Firecrawl MCP configuration for the official [Firecrawl MCP server](https://github.com/firecrawl/firecrawl-mcp-server), so editors that support bundled MCP metadata can wire Firecrawl tools with `FIRECRAWL_API_KEY`.

## Plugins

This repo serves as a plugin for multiple platforms:

- **Claude Code** - `.claude-plugin/`
- **Cursor** - `.cursor-plugin/`
- **OpenAI Codex** - `.codex-plugin/`

## Editing Skills

All current skills in this repo are authored here and can be edited directly in this repo.

If Firecrawl later syncs skills from other repos, that distinction should be documented here and in `AGENTS.md`.

## Prerequisites

- A Firecrawl account or self-hosted Firecrawl deployment
- API key stored in `FIRECRAWL_API_KEY` for cloud usage

Get your API key at [firecrawl.dev/app](https://www.firecrawl.dev/app).

## Relationship To The CLI Repo

Firecrawl has two distinct agent workflows:

1. Agent needs better web tools while doing work.

Install and use the CLI:

```bash
npx -y firecrawl-cli@latest init --all --browser
```

That path installs terminal commands and CLI-native skills for ad hoc web tasks.

2. Agent is building an app that should call Firecrawl.

Use this repo. The skills here focus on:

- getting an API key into `.env`
- choosing fresh project vs existing project flow
- choosing the right endpoint
- asking what Firecrawl should do in the product
- wiring SDKs or REST calls into code
- inspecting an existing repo before integrating
- running a smoke test so the integration is proven, not just written
- avoiding CLI-only guidance when the real task is product integration

Default build flow:

1. decide whether the project is fresh or existing
2. ask what Firecrawl should do in the product
3. route to `/scrape`, `/search`, `/interact`, `/crawl`, or `/map`
4. integrate using the project's existing conventions
5. verify one real Firecrawl request succeeds

## Source Of Truth

This repo intentionally follows the same split described in Firecrawl's onboarding skill:

- Path A: supercharge the agent's own web tooling with the CLI
- Path B: integrate Firecrawl into an application

The onboarding source lives at:

- [`firecrawl-web/public/agent-onboarding/SKILL.md`](https://www.firecrawl.dev/agent-onboarding/SKILL.md)

## Docs

- `/scrape`: [docs.firecrawl.dev/features/scrape](https://docs.firecrawl.dev/features/scrape)
- `/search`: [docs.firecrawl.dev/features/search](https://docs.firecrawl.dev/features/search)
- `/interact`: [docs.firecrawl.dev/features/interact](https://docs.firecrawl.dev/features/interact)
- `/crawl`: [docs.firecrawl.dev/features/crawl](https://docs.firecrawl.dev/features/crawl)
- `/map`: [docs.firecrawl.dev/features/map](https://docs.firecrawl.dev/features/map)

## Scope Boundaries

This repo does not try to duplicate:

- full CLI command references
- terminal flags and output handling rules
- editor setup flows that already belong to `firecrawl/cli`

If a task is "search the web for me right now" or "scrape this URL during the session", point agents to `firecrawl/cli`.
If a task is "add Firecrawl to this codebase", point agents to this repo.

## License

ISC

## Notes

- Evals are intentionally deferred in this first pass while the authored skill set settles.
- If the CLI repo grows more integration-focused material, keep that content high-level there and preserve this repo as the detailed implementation home.
