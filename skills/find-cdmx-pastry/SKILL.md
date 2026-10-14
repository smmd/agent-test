---
name: find-cdmx-pastry
description: >-
  Find sweet-pastry shops in Mexico City from public web results. Use when
  Scout searches for new patisseries, pastelerías, pan dulce, or viennoiserie
  in CDMX neighborhoods.
---

# Skill: Find CDMX pastry

**Loaded by:** [agents/scout.md](../../agents/scout.md)
**Guides:** [tools/web-search.md](../../tools/web-search.md)

Teaches Scout how to search, and which places count. The web-search tool only returns pages. This skill decides what to keep.

## When to load

Scout is looking for new sweet-pastry shops in CDMX.

## Neighborhoods

Start with these, and add another only when the source names it:

- Roma Norte
- Condesa
- Juárez
- Coyoacán
- Centro
- Polanco

## Queries

Run a few short queries. Mix Spanish and English:

- `pastelería nueva {neighborhood} CDMX`
- `pan dulce {neighborhood} Ciudad de México`
- `viennoiserie {neighborhood} Mexico City`
- `bakery opening {neighborhood} CDMX`

## What to keep

- Cakes, cookies, viennoiserie, and traditional Mexican sweet breads.
- A shop whose main offer is sweet pastry.
- A page that places the shop in Mexico City.

## What to drop

- Restaurants that only happen to serve dessert.
- Pages that are not about CDMX.
- A second mention of a shop already in this batch. Keep the clearer source.

## How to write the record

- `source_url` is required. Use the page that was actually opened.
- `why_notable` is one or two sentences taken from that page.
- `address` is filled only when the source prints it. Otherwise leave it `null`.
- `neighborhood` comes from the source. If the source gives none, use the neighborhood from the query and say that in `why_notable`.
- Return 3 to 5 records. Fewer is fine when the sources are thin.

## TODO — next stage

- Send these queries through the real search API in [tools/web-search.md](../../tools/web-search.md).
- Skip names already in the pastry store before they reach Archivist.
