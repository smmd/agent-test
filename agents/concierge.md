# Agent: Concierge

Asks the Dulce Mesa team to visit a saved patisserie and rank it.

| | |
| --- | --- |
| Layer | Agents |
| Reads | Shared records from Archivist, `status: saved` |
| Writes | The same records with `status: notified` |
| Skill | [skills/write-visit-brief/SKILL.md](../skills/write-visit-brief/SKILL.md) |
| Tool | [tools/team-notify.md](../tools/team-notify.md) |
| Must not | Search the web, or change the stored facts about the shop |

## Job

1. Load [write-visit-brief](../skills/write-visit-brief/SKILL.md).
2. Take each saved record.
3. Build one message from that skill's template.
4. Send it with the team-notify tool.
5. If the tool accepts the message, set `status: notified`.
6. If the tool rejects it, leave the record at `saved` and report the failure.

## Rules

- Follow the skill for tone, the empty-address line, and one shop per message.
- Do not mark `notified` unless the tool accepts the message.
- Ranking is a later step. Load [rank-a-visit](../skills/rank-a-visit/SKILL.md) only after a person has visited.

## TODO — next stage

- Pick a channel (Slack, email, or WhatsApp) in [tools/team-notify.md](../tools/team-notify.md).
- Store the team's reply with [rank-a-visit](../skills/rank-a-visit/SKILL.md): rank 1–5 and a one-line note.
- Move `status` from `notified` to `ranked` once that skill has a score.
