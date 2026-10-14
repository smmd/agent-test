---
name: write-visit-brief
description: >-
  Write the Dulce Mesa team note that asks for a visit and a rank. Use when
  Concierge notifies the team about one saved patisserie.
---

# Skill: Write a visit brief

**Loaded by:** [agents/concierge.md](../../agents/concierge.md)
**Guides:** [tools/team-notify.md](../../tools/team-notify.md)

Teaches Concierge how to phrase the note. The notify tool only delivers it.

## When to load

A record is `saved` and the team still needs to hear about it.

## Shape of the note

One shop per message. Use this text:

```text
New patisserie to visit

Name: {name}
Neighborhood: {neighborhood}
Address: {address or "not in the source"}
Why it stood out: {why_notable}
Source: {source_url}

Please visit and reply with a rank from 1 to 5.
```

## Rules

- Copy `why_notable` as stored. Do not add praise.
- If `address` is empty, write `not in the source`.
- Keep the source link in the message.
- Send the note only to the Dulce Mesa team.
- Set `status: notified` only after the tool returns `accepted: true`.

## TODO — next stage

- Fill `channel` once [tools/team-notify.md](../../tools/team-notify.md) picks Slack, email, or WhatsApp.
- Point the reply at [skills/rank-a-visit/SKILL.md](../rank-a-visit/SKILL.md).
