# Freshness and Liveness

A successful scrape tells you what the page returned. It does not prove that the
state represented by the page is current. Keep these two questions separate:

- **Freshness** -> is this content recent, or a cached copy? Controlled by `maxAge`.
- **Liveness** -> is the underlying thing still real and active? Not something a
  scrape can assert on its own.

## The Caching / Freshness Tradeoff (`maxAge`)

Firecrawl reuses recently indexed content to cut latency and cost. `maxAge` is
the maximum age, in milliseconds, of an indexed copy that `/scrape` may return
instead of running the normal scrape path.

- Omitting `maxAge` lets Firecrawl reuse a recent indexed copy. The common
  default window is 2 days, and Firecrawl may tune it for a domain.
- `maxAge: 0` disables index reuse and sends the request through the scrape
  path. It trades latency and reliability for a fresher retrieval.

Keep caching on by default. Pay the `maxAge: 0` latency cost only for the reads
where staleness would cause a wrong or costly decision.

## Freshness-Sensitive Action Checklist

Before an action that depends on current state, treat scrape output as evidence,
not proof:

1. Use `maxAge: 0` for the final retrieval to bypass Firecrawl index reuse.
2. Do not treat HTTP 200 or non-empty content as proof of liveness.
3. Inspect rendered content and redirect evidence. `metadata.sourceURL` is the
   requested URL. When the engine-reported `metadata.url` differs, it can
   indicate a redirect to a different resource. Matching values do not prove no
   redirect occurred.
4. Use source-specific APIs or identifiers where available (they often expose an
   explicit status that a rendered page hides).
5. Treat inconclusive evidence as **unknown**, and stop before the expensive or
   irreversible step, rather than assuming active.

## Worked Example: Collect Current Page Evidence

Neither the status code nor the presence of content settles whether a page's
domain-specific state is current. Bypass index reuse, then collect the rendered
content and response metadata for your application's own validation rules.

```js
import Firecrawl from "@mendable/firecrawl-js";

const firecrawl = new Firecrawl({ apiKey: process.env.FIRECRAWL_API_KEY });

async function collectCurrentPageEvidence(url) {
  // maxAge: 0 bypasses Firecrawl index reuse.
  const doc = await firecrawl.scrape(url, {
    formats: ["markdown"],
    maxAge: 0,
  });

  const requestedURL = doc.metadata?.sourceURL ?? url;
  const responseURL = doc.metadata?.url;

  return {
    markdown: doc.markdown ?? "",
    statusCode: doc.metadata?.statusCode,
    requestedURL,
    responseURL,
    possibleRedirect: Boolean(responseURL && responseURL !== requestedURL),
  };
}

const evidence = await collectCurrentPageEvidence("https://example.com/resource");
// Apply source-specific content, status, API, or identifier checks here.
// If they are inconclusive, keep the state unknown.
```

The important boundary is after collection: Firecrawl supplies page evidence;
your application interprets that evidence using source-specific rules. If those
rules are inconclusive, keep the state `unknown`.

## What Firecrawl Does Not Claim

- HTTP 200 plus content does not prove that the item described by the page is
  still active.
- Firecrawl does not decide whether every kind of item is active. Your
  application makes that decision from the evidence above, in its own terms.
