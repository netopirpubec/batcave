---
name: domain-triage
description: Triage items (issues, tickets, leads, incidents, PRs, anything queued) through a state machine driven by a domain-knowledge brief passed as the skill argument. Use when the user invokes /domain-triage with a multi-sentence or multi-paragraph domain context describing categories, states, and routing rules — or when they ask to triage a queue against domain rules they hand you inline rather than rules baked into the skill. Distinct from /triage, which has its state machine fixed; here the brief is the state machine.
---

# Domain Triage

Triage a queue using a domain-knowledge brief the user passes as the skill argument. The brief is the source of truth — read it carefully, then apply it. Do not import rules from the generic `/triage` skill; this skill is for domains whose triage rules differ.

## The argument

The user invokes `/domain-triage <brief>` where `<brief>` is a paragraph or several paragraphs describing the domain. Expect these elements:

- **What is being triaged** — issues, leads, tickets, incidents, PRs, emails.
- **Where the queue lives** — a tracker, folder, inbox, or list pasted inline.
- **Categories** — the item kinds (bug/enhancement, hot/cold lead, p0/p1/p2…).
- **States** — lifecycle stages and what each means.
- **Routing rules** — how categories and states get decided, and any required ordering of checks.
- **Posting conventions** — disclaimers, templates, language (e.g. SL vs EN), or anything that must appear on every comment.

If the brief is missing one of these and you'll need it, ask once before starting. Don't invent rules the user didn't state.

## Workflow

1. **Restate the brief.** In 4–8 bullets, summarise what you understood: queue location, categories, states, routing rules, posting conventions. Wait for confirmation or correction. This catches misreads before they propagate to every item.

2. **Survey the queue.** Pull the items in scope and bucket them by current state (or "untriaged" if none set). Show counts and a one-line summary per item, oldest first within each bucket. Let the user pick.

3. **Triage the chosen item.**
   - Gather context: read the item fully, plus any prior triage notes. Don't re-ask resolved questions.
   - If the brief calls for verification (reproduction, fit-check, severity test, lead qualification), do that before recommending.
   - Recommend a category and state with reasoning. Quote the specific rule from the brief you applied.
   - Wait for direction.

4. **Apply the outcome.** Execute the state change, post the comment, move the file — whatever the brief defines as "applying" a decision. Confirm the action list before executing.

## Quick override

If the user says "move X to `<state>`", trust them and apply directly. Confirm the action list, then act. Skip grilling.

## When the brief is silent

If the brief doesn't define a rule you need, surface the gap and propose a default — don't invent silently. Common gaps: items matching multiple categories, items older than N days, attribution on auto-generated comments, what closes versus archives.

## Resuming

If prior triage notes exist on an item, read them, check for activity since they were posted, and present an updated picture before continuing. Don't re-ask resolved questions.
