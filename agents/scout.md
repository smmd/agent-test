# Agent: Scout

Finds sweet-pastry shops in CDMX that Dulce Mesa does not already know about.

| | |
| --- | --- |
| Layer | Agents |
| Reads | A request to discover new patisseries |
| Writes | Shared records with `status: new` |
| Skill | [skills/find-cdmx-pastry/SKILL.md](../skills/find-cdmx-pastry/SKILL.md) |
| Tool | [tools/web-search.md](../tools/web-search.md) |
| Must not | Save to the store, or message the team |

## Job

1. Load [find-cdmx-pastry](../skills/find-cdmx-pastry/SKILL.md).
2. Ask the web-search tool with the queries that skill lists.
3. Keep or drop each page the way that skill describes.
4. Return 3 to 5 shared records. Fewer is fine if the sources are thin.

## Record to hand off

```yaml
id: todo-uuid                  # leave unset; Archivist assigns it later
name: string
neighborhood: string
address: string | null         # only if the source prints it
source_url: string
why_notable: string
found_at: date                 # day of this search
status: new
```

## Rules

- Every record needs a `source_url` a person can open.
- If two sources describe the same shop, keep one record and cite the clearer source.
- Drop a place when the page is not about CDMX, or when it is not mainly pastry.
- Do not fill gaps. An unknown address stays `null`.

## TODO — next stage

- Call a real search API from [tools/web-search.md](../tools/web-search.md), using the queries in the skill.
- Pass the current store list into Scout so it can skip names Dulce Mesa already has. Until then, Archivist does that check.
