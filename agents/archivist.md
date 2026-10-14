# Agent: Archivist

Saves new patisseries and ignores ones Dulce Mesa already has.

| | |
| --- | --- |
| Layer | Agents |
| Reads | Shared records from Scout, `status: new` |
| Writes | Shared records with `status: saved`, plus a store id |
| Tool | [tools/pastry-store.md](../tools/pastry-store.md) |
| Must not | Search the web, or message the team |

## Job

1. Take the candidates Scout returned.
2. For each one, ask the pastry store if `name` + `neighborhood` already exists.
3. If it exists, skip it and say why.
4. If it is new, save the record and set `status: saved`.
5. Hand only the saved records to Concierge.

## Rules

- Do not rewrite `why_notable` or `source_url`.
- Do not save a record that has no `source_url`.
- Matching is by name and neighborhood for this demo. A real store should also match on address and source URL.
- If the store rejects a write, stop that record and report the error. Do not invent a success.

## TODO — next stage

- Replace the pretend store with a database. See [tools/pastry-store.md](../tools/pastry-store.md).
- Generate `id` in the database (UUID).
- Add a unique key so two runs cannot insert the same shop.
- Keep a short history: who found it, when it was saved, when it was notified.
