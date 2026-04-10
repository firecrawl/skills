# SDK Installation

Install the SDK that matches the project language. Prefer the language already used by the app.

For existing projects, inspect the repo first and match its package manager, dependency conventions, and where third-party API clients already live.

## JavaScript / TypeScript

```bash
npm install @mendable/firecrawl-js
```

## Python

```bash
pip install firecrawl-py
```

## REST

Use direct HTTP calls when:

- the project language does not have an official SDK in scope
- the existing networking layer already wraps third-party APIs
- the integration needs a minimal dependency footprint

After installation, run a smoke test from the real integration path. See [verification.md](verification.md).

Canonical docs (source of truth for all endpoint details):

- [docs.firecrawl.dev/features/scrape](https://docs.firecrawl.dev/features/scrape)
- [docs.firecrawl.dev/features/search](https://docs.firecrawl.dev/features/search)
- [docs.firecrawl.dev/features/interact](https://docs.firecrawl.dev/features/interact)
- [docs.firecrawl.dev/features/crawl](https://docs.firecrawl.dev/features/crawl)
- [docs.firecrawl.dev/features/map](https://docs.firecrawl.dev/features/map)
