---
name: rank-a-visit
description: >-
  Score a Dulce Mesa visit from 1 to 5 and write the rank back on the pastry
  record. Use after the team has visited a notified patisserie.
---

# Skill: Rank a visit

**Loaded by:** no agent yet. This is the step after `notified`.
**Guides:** [tools/pastry-store.md](../../tools/pastry-store.md), once a rank can be saved.

Teaches a later ranking step how to turn a visit into a score. Discover-patisseries stops at the team note. This skill starts the next loop.

## When to load

Someone on the team has visited a shop and is ready to rank it.

## Stop

- If the reply has no number from 1 to 5, ask and wait. Do not invent a score.
- Do not write the rank until the plan in [CLAUDE.md](../../CLAUDE.md) has a yes.

## Score four things, each from 1 to 5

| Score | Question |
| --- | --- |
| Pastry | How good was the sweet pastry itself? |
| Consistency | Did the shop seem reliable, not a one-off good item? |
| Trip | Was it worth the trip inside that neighborhood? |
| Recommend | Would Dulce Mesa recommend it? |

## Overall rank

Use one rank from 1 to 5 for the record:

| Rank | Meaning |
| --- | --- |
| 5 | Recommend without hesitation |
| 4 | Recommend |
| 3 | Worth a visit, with a caveat |
| 2 | Skip unless already nearby |
| 1 | Do not recommend |

Add one line on what to order, or why to skip it.

## Record after a rank

```yaml
status: ranked
rank: 1-5
visit_note: string
ranked_at: date
```

Leave `name`, `neighborhood`, `source_url`, and `why_notable` unchanged.

## TODO — next stage

- Add an agent that reads the team reply and loads this skill.
- Store `rank`, `visit_note`, and `ranked_at` on the table in [tools/pastry-store.md](../../tools/pastry-store.md).
- Publish ranked places into a recommendation list. That list is not part of this example.
