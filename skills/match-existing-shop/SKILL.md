---
name: match-existing-shop
description: >-
  Decide whether a pastry candidate is already in the Dulce Mesa store. Use
  when Archivist checks a new record for a duplicate by name, neighborhood,
  address, or source URL.
---

# Skill: Match an existing shop

**Loaded by:** [agents/archivist.md](../../agents/archivist.md)
**Guides:** [tools/pastry-store.md](../../tools/pastry-store.md)

Teaches Archivist when two mentions are the same shop. The pastry store only looks up and saves. This skill decides the match.

## When to load

Archivist has a candidate with `status: new` and needs to know if Dulce Mesa already has it.

## Treat as the same shop

- Same name and same neighborhood.
- Same address, even when the name is shortened.
- Same `source_url`.
- Differences that are only spelling: accents (`Coyoacán` / `Coyoacan`), `Panadería` versus `Pastelería`, or `y` versus `&`.

## Treat as a new shop

- Same name in a different neighborhood, unless the address shows it is one shop.
- A clearly different place that only shares a neighborhood.

## When unsure

Do not save a second row. Hand the candidate back as a possible duplicate and name the existing record it might match.

## Before saving

- Refuse a record with no `source_url`.
- Copy `why_notable` and `source_url` as Scout wrote them.
- Set `status: saved` only after the store accepts the write.

## TODO — next stage

- Back this match with the unique key planned in [tools/pastry-store.md](../../tools/pastry-store.md).
- Compare a normalized name (lowercase, accents removed) in the database.
