# Workflow: Discover new patisseries

**Owner:** Dulce Mesa
**Trigger:** Someone asks to find new patisseries in CDMX.
**Agents, in order:** Scout, then Archivist, then Concierge.

## Goal

Bring a short list of new sweet-pastry places to the team, so they can visit and rank them. This workflow ends when the team has been notified. It does not collect the rank.

## Steps

### 1. Scout

- Read [agents/scout.md](../agents/scout.md).
- Search for patisseries in CDMX that look new or newly talked about.
- Return 3 to 5 candidates as shared records with `status: new`.
- If the search returns nothing useful, stop. Do not call Archivist or Concierge.

### 2. Archivist

- Read [agents/archivist.md](../agents/archivist.md).
- For each candidate, check the store for the same name and neighborhood.
- Save only the new ones and set `status: saved`.
- If every candidate is already stored, stop. Do not call Concierge.

### 3. Concierge

- Read [agents/concierge.md](../agents/concierge.md).
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

- Accept a reply from the team (visited / ranked / skip) and update the record.
- Publish ranked places into a recommendation list.
- Schedule this workflow (for example, once a week) instead of running it by hand.
