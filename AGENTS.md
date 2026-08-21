# Firecrawl Skills Catalog

Read-only distribution catalog for all Firecrawl agent skills. **Every skill directory here is a CI-synced mirror. You must not edit skills in this repo.**

## Layout and sources

- `skills/core/` — mirror of `firecrawl/cli` `skills/` (core skills: Firecrawl primitives via CLI/MCP + the research/developer index skills)
- `skills/build/` — mirror of the `firecrawl` monorepo `skills/`
- `skills/workflows/` — mirror of `firecrawl/firecrawl-workflows` `skills/`

Only repo metadata is authored here: `.cursor-plugin/`, `.claude-plugin/`, `.codex-plugin/`, `README.md`, `AGENTS.md`, `.mcp.json`, `mcp.json`, `.github/`.

## Routing rule

Core skills (including the research/developer index skills) → PR `firecrawl/cli`. Build/SDK skills → PR `firecrawl` (monorepo, `skills/`). Workflow skills → PR `firecrawl/firecrawl-workflows`. Never PR skill content against this catalog — CI overwrites it on the next sync.

## Intent

Use the skills here when the task is:

- live web work during a session, or querying the research paper / developer indexes (core skills)
- adding Firecrawl to a codebase, choosing between `/scrape`, `/search`, and `/interact`, getting `FIRECRAWL_API_KEY` into `.env` (build skills)
- end-to-end recipes like lead gen, deep research, SEO audits (workflow skills)
