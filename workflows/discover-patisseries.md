# Workflow: Discover new patisseries

**Owner:** Dulce Mesa
**Trigger:** Someone asks to find new patisseries in CDMX.
**Agents, in order:** Scout, then Archivist, then Concierge.

## Goal

Bring a short list of new sweet-pastry places to the team, so they can visit and rank them. This workflow ends when the team has been notified. It does not collect the rank.

## Steps

### 0. Clarify and plan

- Read the standing rules in [CLAUDE.md](../CLAUDE.md).
- If a clarify case is open, ask one question and stop.
- Post the plan (`Goal`, `Will call`, `Will not call`, `Open questions`) and wait for a yes.
- Scout may search while that plan is being written, so the plan can name real shops.
- Archivist does not save, and Concierge does not notify, until the same yes covers their tools.

### 1. Scout

- Read [agents/scout.md](../agents/scout.md) and load [find-cdmx-pastry](../skills/find-cdmx-pastry/SKILL.md).
- Search for patisseries in CDMX that look new or newly talked about.
- Return 3 to 5 candidates as shared records with `status: new`.
- If the search returns nothing useful, stop. Do not call Archivist or Concierge.

### 2. Archivist

- Read [agents/archivist.md](../agents/archivist.md) and load [match-existing-shop](../skills/match-existing-shop/SKILL.md).
- For each candidate, check the store with that skill's match.
- Save only the new ones and set `status: saved`.
- If every candidate is already stored, stop. Do not call Concierge.

### 3. Concierge

- Read [agents/concierge.md](../agents/concierge.md) and load [write-visit-brief](../skills/write-visit-brief/SKILL.md).
- Send one notification per saved record.
- Set `status: notified` after the note is accepted.
- The message asks the team to visit and rank the place from 1 to 5.

## Done when

- Every saved place is `notified`, or the workflow stopped earlier because there was nothing new.
- The handoff still carries `name`, `neighborhood`, `source_url`, and `why_notable`.

## Out of this example

- No one visits the shop inside this workflow.
- No score is written back.
- No customer-facing recommendation is published.

## TODO — next stage

- Accept a reply from the team and score it with [rank-a-visit](../skills/rank-a-visit/SKILL.md).
- Publish ranked places into a recommendation list.
- Schedule this workflow (for example, once a week) instead of running it by hand.
