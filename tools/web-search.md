# Tool: Web search

**Used by:** [agents/scout.md](../agents/scout.md)
**Status:** Contract only. No API is connected.

## Purpose

Search the public web for sweet-pastry shops in CDMX.

## Input

```yaml
query: string                  # example: "pastelería nueva Roma Norte CDMX"
limit: number                  # Scout asks for a small set, then keeps 3 to 5
```

## Output

```yaml
results:
  - title: string
    url: string
    snippet: string
    published_at: date | null
```

Scout turns these results into shared records. This tool does not decide which shops to keep.

## Rules for a later implementation

- Search public pages only.
- Return the URL that was actually opened.
- Do not scrape behind a login.

## TODO — next stage

- Connect a search API (or a small allowlist of food and city sites).
- Cache results for a day so a repeated demo does not hammer the API.
- Log the query and the URLs returned, so a presenter can show the source of each shop.
