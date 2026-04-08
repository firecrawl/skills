# Endpoint Selection

Use the narrowest endpoint that matches the feature:

| Endpoint | Use when | Do not start here when |
|---|---|---|
| `/scrape` | You already have the URL and need one page | The feature starts with a query or needs many pages |
| `/search` | The feature starts with a query and must discover sources | The target site and URL are already known |
| `/interact` | The page must be clicked, typed into, or navigated after scrape | Plain `/scrape` already returns the data |
| `/crawl` | You need many related pages from one site section | You only need one or a few known URLs |
| `/map` | You know the site but not the exact URLs yet | A general web query is still needed |

Default priority for most product integrations:

1. `/scrape`
2. `/search`
3. `/interact`
4. `/crawl`
5. `/map`

Escalation rules:

- Start with `/scrape` before `/interact`.
- Start with `/search` when URL discovery is part of the product behavior.
- Use `/map` before `/crawl` when URL discovery on a single site is the main task.
