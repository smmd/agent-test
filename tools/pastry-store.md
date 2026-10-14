# Tool: Pastry store

**Used by:** [agents/archivist.md](../agents/archivist.md)
**Status:** Contract only. No database is connected.

For this presentation, reads and writes are pretend. Archivist describes what it would save. Nothing is persisted.

## Purpose

Remember patisseries Dulce Mesa already knows, and accept new ones.

## Operations

### Find existing

```yaml
input:
  name: string
  neighborhood: string
output:
  found: boolean
  id: string | null
```

Match on name and neighborhood. Address and `source_url` can join the match later.

### Save

```yaml
input:
  name: string
  neighborhood: string
  address: string | null
  source_url: string
  why_notable: string
  found_at: date
  status: saved
output:
  id: string
  status: saved
```

## Rules for a later implementation

- Require `source_url` before insert.
- Refuse a second row with the same name and neighborhood.
- Return the existing `id` when the row is already there, so Archivist can skip it.

## TODO — next stage

- Create a table, for example in Postgres:

  ```text
  patisseries
    id            uuid
    name          text
    neighborhood  text
    address       text null
    source_url    text
    why_notable   text
    found_at      date
    status        text
    rank          int null          # 1–5, filled after a visit
    unique (name, neighborhood)
  ```

- Point Archivist at this table through a small client.
- Add `notified_at` and `ranked_at` when those steps exist.
