# Agent: Concierge

Asks the Dulce Mesa team to visit a saved patisserie and rank it.

| | |
| --- | --- |
| Layer | Agents |
| Reads | Shared records from Archivist, `status: saved` |
| Writes | The same records with `status: notified` |
| Tool | [tools/team-notify.md](../tools/team-notify.md) |
| Must not | Search the web, or change the stored facts about the shop |

## Job

1. Take each saved record.
2. Build one short message (template below).
3. Send it with the team-notify tool.
4. If the tool accepts the message, set `status: notified`.
5. If the tool rejects it, leave the record at `saved` and report the failure.

## Message template

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

- One message per shop. Do not bundle several shops into one note.
- Do not add praise that is not in `why_notable`.
- Do not mark `notified` unless the tool accepts the message.
- Ranking is a human step. This agent only asks for it.

## TODO — next stage

- Pick a channel (Slack, email, or WhatsApp) in [tools/team-notify.md](../tools/team-notify.md).
- Store the team's reply: visited date, rank 1–5, and a one-line note.
- Move `status` from `notified` to `visited`, then to `ranked`.
