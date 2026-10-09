---
name: delegate-with-handoff
description: Use when you have a task to carry out and the runtime can start sub-agents - define the task first, then hand it to a fresh agent with no inherited context, on the cheapest model that can do it, with a written handoff carrying exactly the knowledge it needs; you stay the orchestrator and verify the result.
type: Skill
title: Delegate With Handoff
status: draft
---

# Delegate With Handoff

## Overview

The orchestrator (you) holds the conversation, the decisions and the user. Workers do the
tasks. Each worker starts empty - no conversation history, no inherited context - so it
costs only what its task needs, and the cheapest model able to do it is the one used.
Everything the worker must know travels in a written handoff.

## 1. Define the task before dispatching

A worker cannot ask what you meant. Before starting one, write down:

- **Objective** - one sentence, the outcome rather than the steps.
- **Scope** - the files, directories or systems it may touch, and what it must not touch.
- **Done when** - observable acceptance criteria: tests that pass, a command's output, a
  screenshot that shows X.
- **Verification** - the exact commands it runs to prove the criteria.

If any of these is unclear, settle it first (with the user if it is their call). A vague
task delegated is a wasted run.

## 2. Pick the cheapest capable worker

Choose the smallest model and effort that can do the task in one pass:

| Task | Worker |
|------|--------|
| Search, inventory, read-and-summarise, mechanical edits, renames, running checks | smallest / fastest model, low effort |
| Ordinary feature work or bug fix with a clear spec | mid-tier model |
| Hard design, tricky debugging, security-sensitive change | top model, only when the cheaper one would likely fail |

Independent tasks go to parallel workers; dependent ones run in sequence.

## 3. Write the handoff

The handoff is the worker's whole world. Include only what it needs:

```
Task: <objective>
Context: <the few facts it needs: where the code lives, conventions, decisions already taken and why>
Files: <paths to read first; paths it may change>
Constraints: <what not to touch, style rules, no commits/pushes unless stated, secrets rules>
Done when: <acceptance criteria>
Verify with: <commands>
Report back: <what changed (files), verification output, anything left open - short>
```

Point to files rather than pasting them; paste only what the worker cannot read itself
(conversation decisions, user preferences, screenshots described in words). Never put
secrets in a handoff.

## 4. Check the result

The worker's report is a claim, not proof. Read the diff, rerun the verification, and look
at the result yourself (screenshot, output) before telling the user it is done. If it fell
short, send a follow-up to the same worker with what is missing, or redo it yourself when
the fix is smaller than another handoff.

## When not to delegate

- The work is smaller than the handoff (a one-line edit, a single command): do it inline.
- The task needs live back-and-forth with the user or decisions not yet made.
- The task needs the whole conversation to make sense and cannot be summarised.

## Red flags

- Dispatching with "fix the layout" and no acceptance criteria.
- Defaulting to the most capable model for a mechanical task.
- Forwarding the whole conversation instead of a handoff.
- Relaying the worker's "done" to the user without checking it.
