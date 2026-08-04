# Auth And Environment

## Hosted Firecrawl (with API key)

For hosted Firecrawl with full API access, set:

```dotenv
FIRECRAWL_API_KEY=fc-...
```

## Keyless access (no API key)

Hosted Firecrawl and the [Firecrawl MCP server](https://github.com/firecrawl/firecrawl-mcp-server) support **keyless** access when no credential is configured. In this mode, a limited set of tools can run without `FIRECRAWL_API_KEY` or OAuth:

- `firecrawl_scrape`
- `firecrawl_search`
- `firecrawl_parse`

- Do **not** treat a missing `FIRECRAWL_API_KEY` as a hard error when keyless access is sufficient for the task.
- `/interact` and other advanced endpoints require credentials (API key or OAuth).
- If the user needs tools beyond the keyless set, obtain credentials via this skill's onboarding flow or configure OAuth/API key auth.
- The MCP server declares `FIRECRAWL_API_KEY` as optional in `server.json` (`isRequired: false`).

## Self-hosted Firecrawl

For self-hosted Firecrawl, set:

```dotenv
FIRECRAWL_API_URL=https://your-firecrawl-instance.example.com
```

Guidelines:

- Never hardcode the API key in source files.
- Prefer `.env` or the deployment platform's secret manager.
- Only set `FIRECRAWL_API_URL` when the project is not using `https://api.firecrawl.dev`.
- If the user needs interactive authorization, follow the onboarding flow in `firecrawl-build-onboarding`.
