---
name: domain-triage
description: Triage items (issues, tickets, leads, incidents, PRs, anything queued) through a state machine driven by a domain-knowledge brief passed as the skill argument. Use when the user invokes /domain-triage with a multi-sentence or multi-paragraph domain context describing categories, states, and routing rules — or when they ask to triage a queue against domain rules they hand you inline rather than rules baked into the skill. Distinct from /triage, which has its state machine fixed; here the brief is the state machine.
---

# Domain Triage

Triage a queue using the brief the user passes as argument. The brief is the source of truth. Don't import rules from `/triage`.

## The argument

`/domain-triage <brief>` should describe:

- **What** is triaged (issues, leads, tickets, incidents, PRs, emails).
- **Where** the queue lives (tracker, folder, inbox, inline list).
- **Categories** (bug/enhancement, hot/cold, p0/p1/p2…).
- **States** and what each means.
- **Routing rules** — how category/state are decided, plus any required ordering.
- **Posting conventions** — disclaimers, templates, language, required boilerplate.

If something you'll need is missing, ask once. Don't invent rules.

## Workflow

1. **Restate the brief** in 4–8 bullets (queue, categories, states, routing, posting). Wait for confirmation — catches misreads before they propagate.

2. **Survey the queue.** Pull in-scope items, bucket by current state (or "untriaged"). Show counts and a one-line summary per item, oldest first per bucket. Let the user pick.

3. **Triage the chosen item.**
   - Read it fully plus prior triage notes; don't re-ask resolved questions.
   - If the brief requires verification (repro, fit-check, severity, qualification), do it first.
   - Recommend category + state with reasoning, quoting the specific rule applied.
   - Wait for direction.

4. **Apply the outcome.** Execute the state change / comment / move per the brief's "apply" definition. Confirm the action list before executing.

## Quick override

If the user says "move X to `<state>`", trust them. Confirm the action list, then act. Skip grilling.

## When the brief is silent

Surface the gap and propose a default — don't invent silently. Common gaps: multi-category items, age cutoffs, comment attribution, close vs archive.

## Resuming

If prior triage notes exist, read them, check for activity since, and present an updated picture before continuing. Don't re-ask resolved questions.
