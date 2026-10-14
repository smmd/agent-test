# Tool: Team notify

**Used by:** [agents/concierge.md](../agents/concierge.md)
**Status:** Contract only. No message is sent.

## Purpose

Deliver one visit request to the Dulce Mesa team.

## Input

```yaml
channel: string                # undecided: slack | email | whatsapp
subject: string                # "New patisserie to visit"
body: string                   # the template in agents/concierge.md
record_id: string              # the id Archivist saved
```

## Output

```yaml
accepted: boolean
channel_message_id: string | null
```

`accepted: true` means the channel took the message. Concierge may then set `status: notified`. `accepted: false` means the record stays `saved`.

## Rules for a later implementation

- Send only to the Dulce Mesa team list. Do not message customers.
- One shop per message.
- Keep `channel_message_id` so a later stage can attach the team's rank to the same record.

## TODO — next stage

- Choose the channel and add its webhook or mail client here.
- Define the reply the team sends back: `rank` from 1 to 5, plus an optional note.
- Write that reply onto the pastry store and set `status: ranked`.
