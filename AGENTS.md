# Firecrawl Skills Repo

Distribution repo for Firecrawl agent skills focused on the application-integration path.

## Safe to edit

All current skills in this repo are authored here:

- `skills/firecrawl-build/`
- `skills/firecrawl-build-onboarding/`
- `skills/firecrawl-build-scrape/`
- `skills/firecrawl-build-search/`
- `skills/firecrawl-build-interact/`

Plugin metadata and top-level docs are also safe to edit:

- `.cursor-plugin/`
- `.claude-plugin/`
- `.codex-plugin/`
- `README.md`
- `AGENTS.md`
- `.mcp.json`
- `mcp.json`

## Intent

Prefer these skills when the task is:

- adding Firecrawl to a codebase
- choosing between `/scrape`, `/search`, and `/interact`
- getting `FIRECRAWL_API_KEY` into `.env`
- selecting SDKs or REST patterns for product code

Do not use this repo as the primary source for:

- one-off web research
- ad hoc scraping during the current coding session
- terminal command reference

Those workflows use the CLI skills, which are installed alongside these
build skills by the same `firecrawl init` command.

## Authoring Rules

- Keep each `SKILL.md` concise and trigger-oriented.
- Lead with "use this when..." guidance.
- Favor endpoint names in slash notation: `/scrape`, `/search`, `/interact`.
- Keep CLI references short and defer to `firecrawl/cli` instead of duplicating command manuals.
- Treat [`https://www.firecrawl.dev/agent-onboarding/SKILL.md`](https://www.firecrawl.dev/agent-onboarding/SKILL.md) as the canonical source for the two-path framing.

## Coverage Priority

Current priority order:

1. `/scrape`
2. `/search`
3. `/interact`

## Repo Shape

Expected layout:

- `skills/<skill-name>/SKILL.md` for the skill itself
- `skills/<skill-name>/references/` for deeper docs and recipes
- plugin metadata under `.cursor-plugin/`, `.claude-plugin/`, and `.codex-plugin/`
- top-level docs in `README.md` and this file

Keep supporting references one level deep.
