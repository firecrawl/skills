# Firecrawl Skills Catalog

Distribution catalog for all Firecrawl agent skills. **Every directory under `skills/` is a CI-synced mirror. You must not edit files under `skills/` in this repository.**

## Layout and sources

- `skills/core/` — mirror of `firecrawl/cli` `skills/` (core skills: Firecrawl primitives via CLI/MCP + the research/developer index skills)
- `skills/build/` — mirror of the `firecrawl` monorepo `skills/`
- `skills/workflows/` — mirror of `firecrawl/firecrawl-workflows` `skills/`

Repository-level metadata is authored here, including `.cursor-plugin/`, `.claude-plugin/`, `.codex-plugin/`, `README.md`, `AGENTS.md`, `CLAUDE.md`, `LICENSE`, `.mcp.json`, `mcp.json`, and `.github/`.

## Routing rule

Core skills, including the research and developer index skills, belong in `firecrawl/cli`. Build and SDK skills belong in the `firecrawl` monorepo under `skills/`. Workflow skills belong in `firecrawl/firecrawl-workflows`. Do not submit changes to files under `skills/` in this catalog. CI replaces those directories during the next source sync.

## Intent

Use the skills here when the task is:

- live web work during a session, or querying the research paper / developer indexes (core skills)
- adding Firecrawl to a codebase, choosing between `/scrape`, `/search`, and `/interact`, getting `FIRECRAWL_API_KEY` into `.env` (build skills)
- end-to-end recipes like lead gen, deep research, SEO audits (workflow skills)
