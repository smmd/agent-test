# Dulce Mesa

Dulce Mesa is a small desk that recommends sweet pastries in Mexico City (CDMX). This file is the rulebook for a presentation example. It is not a running system.

The work is split into three layers:

| Layer | Where it lives | What it does |
| --- | --- | --- |
| Workflows | `workflows/` | The order of work and the handoff between agents |
| Agents | `agents/` | Who does each step, and which tools they may use |
| Tools | `tools/` | The contracts those agents call. Nothing here is wired up yet |

## Main workflow

When someone asks to find new patisseries, follow [workflows/discover-patisseries.md](workflows/discover-patisseries.md).

```text
Scout  -->  Archivist  -->  Concierge
search      save            notify the team
```

1. **Scout** looks on the public web for patisseries in CDMX.
2. **Archivist** keeps the ones that are not already stored.
3. **Concierge** asks the team to visit and rank each saved place.

## Rules

- Stay inside sweet pastries in CDMX. Neighborhoods, bakeries, and pastry shops are in scope. Restaurants that do not center on pastry are out of scope.
- Do not invent addresses, hours, prices, or reviews. If a source does not say it, leave the field empty and say so.
- Agents do not skip ahead. Scout does not write the store. Archivist does not notify the team. Concierge does not search the web.
- An agent may use only the tools listed on its own card.
- Pass the shared record below from one agent to the next. Do not drop `source_url`.
- This demo stops at `notified`. Visiting and ranking happen later, with people.

## Shared record

```yaml
id: todo-uuid
name: string
neighborhood: string          # Roma Norte, Condesa, Coyoacán, ...
address: string | null
source_url: string
why_notable: string           # one or two sentences, from the source
found_at: date
status: new | saved | notified | visited | ranked
```

## Agents

| Agent | File | Tool |
| --- | --- | --- |
| Scout | [agents/scout.md](agents/scout.md) | [tools/web-search.md](tools/web-search.md) |
| Archivist | [agents/archivist.md](agents/archivist.md) | [tools/pastry-store.md](tools/pastry-store.md) |
| Concierge | [agents/concierge.md](agents/concierge.md) | [tools/team-notify.md](tools/team-notify.md) |

## TODO — make this real

- Replace each tool note with a real client (search API, database, notification channel).
- Give each agent a runtime that reads its card and is allowed to call only its tool.
- Store the shared record in a database and generate `id` there.
- After a visit, write `status: ranked` and a score from 1 to 5. That loop is not in this example.
