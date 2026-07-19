# Freshness and Liveness

A successful scrape tells you what the page returned. It does not prove that the
item described by the page (a job posting, a listing, an account state) is still
active. Keep these two questions separate:

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

Before an expensive or irreversible action (applying, purchasing, sending),
treat scrape output as evidence, not proof:

1. Use `maxAge: 0` for the final retrieval to bypass Firecrawl index reuse.
2. Do not treat HTTP 200 or non-empty content as proof of liveness.
3. Inspect rendered content and redirect evidence. `metadata.sourceURL` is the
   requested URL. When the engine-reported `metadata.url` differs, it can
   indicate a redirect; a redirect to a generic listing or board page is
   evidence of removal. Matching values do not prove no redirect occurred.
4. Use source-specific APIs or identifiers where available (they often expose an
   explicit status that a rendered page hides).
5. Treat inconclusive evidence as **unknown**, and stop before the expensive or
   irreversible step, rather than assuming active.

## Worked Example: Is This Job Posting Still Open?

Applicant tracking systems make this trap concrete:

- Ashby can return HTTP 200 while rendering "Job not found."
- Greenhouse can redirect a removed posting to a generic board page that also
  returns HTTP 200.

So neither the status code nor the presence of content settles it. Bypass index
reuse, then classify against the rendered markdown and any response URL reported
by the scrape engine.

```js
import Firecrawl from "@mendable/firecrawl-js";

const firecrawl = new Firecrawl({ apiKey: process.env.FIRECRAWL_API_KEY });

const REMOVAL_PHRASES = [
  "job not found",
  "position has been filled",
  "no longer accepting applications",
  "this job is no longer available",
];

async function classifyPosting(url) {
  // maxAge: 0 bypasses Firecrawl index reuse.
  const doc = await firecrawl.scrape(url, {
    formats: ["markdown"],
    maxAge: 0,
  });

  const markdown = (doc.markdown ?? "").toLowerCase();
  const statusCode = doc.metadata?.statusCode;
  const responseURL = doc.metadata?.url ?? url;

  // Redirect away from the requested URL to a generic board is removal evidence.
  const redirectedToBoard =
    responseURL !== url && !responseURL.includes(new URL(url).pathname);

  if (REMOVAL_PHRASES.some(phrase => markdown.includes(phrase))) {
    return { state: "removed", reason: "removal phrase in content" };
  }
  if (redirectedToBoard) {
    return { state: "removed", reason: `redirected to ${responseURL}` };
  }
  if (statusCode && statusCode >= 400) {
    return { state: "removed", reason: `status ${statusCode}` };
  }

  // HTTP 200 + content is not a positive signal that the posting is open.
  return { state: "unknown", reason: "no positive liveness signal" };
}

const result = await classifyPosting(postingURL);
if (result.state !== "active" /* e.g. confirmed via the ATS API */) {
  // Do not submit an application on "unknown". Surface it or re-check.
}
```

The important line is the last branch: `active`, `removed`, and `unknown` are
distinct. A scrape that succeeds but shows no positive signal is `unknown`, not
`active`. Where the ATS exposes an API or a status field, prefer it over parsing
rendered text (step 4).

## What Firecrawl Does Not Claim

- HTTP 200 plus content does not prove that the item described by the page is
  still active.
- Firecrawl does not decide whether every kind of item is active. Your
  application makes that decision from the evidence above, in its own terms.
