# Dulce Mesa

Dulce Mesa is a small desk that recommends sweet pastries in Mexico City (CDMX). This file is the rulebook for a presentation example. It is not a running system.

The work is split into four layers:

| Layer | Where it lives | What it does |
| --- | --- | --- |
| Workflows | `workflows/` | The order of work and the handoff between agents |
| Agents | `agents/` | Who does each step |
| Skills | `skills/` | How that agent does the craft |
| Tools | `tools/` | The external action the skill guides. Nothing here is wired up yet |

## Standing rules

These two rules come before the workflow. Every agent follows them.

### Ask, then wait

Ask one short question and stop when any of these are true:

- The request names no neighborhood and does not say "anywhere in CDMX".
- A page might not be a pastry shop.
- Archivist is unsure whether two mentions are the same shop.
- A rank reply has no number from 1 to 5.
- The next step would save, notify, or store a rank, and nobody has confirmed the plan.

Leave the unknown field empty. Do not guess an address, a neighborhood, or a rank.

### Plan before build

Build means a write: saving a shop, sending the team note, or storing a rank. Search may happen while planning. A write may not.

Before any write, post this plan and wait for a yes:

```text
Goal:
Will call:
Will not call:
Open questions:
```

Archivist, Concierge, and the later ranking step refuse to write until that plan has a yes. If the yes changes the goal, write the plan again.

This is the insurance policy: saves in `pastry-store` and sends in `team-notify` stay closed until the plan is confirmed.

## Main workflow

When someone asks to find new patisseries, follow [workflows/discover-patisseries.md](workflows/discover-patisseries.md).

```text
(first)     clarify, write the plan, wait for a yes
Scout       loads find-cdmx-pastry       calls web-search
Archivist   loads match-existing-shop    calls pastry-store
Concierge   loads write-visit-brief      calls team-notify
(later)     loads rank-a-visit           writes the score
```

1. **Clarify and plan.** Ask if a standing rule is open. Post the plan. Wait for a yes before any write.
2. **Scout** looks on the public web for patisseries in CDMX.
3. **Archivist** keeps the ones that are not already stored.
4. **Concierge** asks the team to visit and rank each saved place.
5. **Rank a visit** is the next loop. No agent owns it yet. It still waits for a yes before it writes a score.

## Rules

- Stay inside sweet pastries in CDMX. Neighborhoods, bakeries, and pastry shops are in scope. Restaurants that do not center on pastry are out of scope.
- Do not invent addresses, hours, prices, or reviews. If a source does not say it, leave the field empty and say so.
- Agents do not skip ahead. Scout does not write the store. Archivist does not notify the team. Concierge does not search the web.
- An agent loads only the skill on its card, and that skill may guide only the tool on that card.
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

## Agents and skills

| Agent | File | Skill | Tool |
| --- | --- | --- | --- |
| Scout | [agents/scout.md](agents/scout.md) | [find-cdmx-pastry](skills/find-cdmx-pastry/SKILL.md) | [web-search](tools/web-search.md) |
| Archivist | [agents/archivist.md](agents/archivist.md) | [match-existing-shop](skills/match-existing-shop/SKILL.md) | [pastry-store](tools/pastry-store.md) |
| Concierge | [agents/concierge.md](agents/concierge.md) | [write-visit-brief](skills/write-visit-brief/SKILL.md) | [team-notify](tools/team-notify.md) |
| (later) | — | [rank-a-visit](skills/rank-a-visit/SKILL.md) | pastry-store, when a rank can be saved |

## TODO — make this real

- Replace each tool note with a real client (search API, database, notification channel).
- Give each agent a runtime that reads its card and is allowed to call only its tool.
- Store the shared record in a database and generate `id` there.
- After a visit, load [rank-a-visit](skills/rank-a-visit/SKILL.md), write `status: ranked`, and store a score from 1 to 5. That loop is not in this example.
