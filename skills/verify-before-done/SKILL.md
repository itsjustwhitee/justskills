---
name: verify-before-done
description: Use before telling the user something works, is fixed, passes, or is complete - and before committing or marking a task done.
type: Skill
title: Verify Before Done
status: draft
---

# Verify Before Done

## Overview

No completion claim without fresh verification evidence from this session. "It
works" / "fixed" / "tests pass" / "done" are claims about the current state, so
they need a command you just ran, not a memory of one.

## The gate

1. **Identify** - which command proves this claim?
2. **Run** - execute it in full, fresh, no caching, no partial scope.
3. **Read** - the whole output: exit code, failure count, warnings.
4. **Verify** - does the output actually confirm the claim, not just "look ok"?
5. **Then** - make the claim, quoting the evidence (command + key line).

Skipping a step is guessing, not verifying.

## Rationalization table

| Excuse | Reality |
|--------|---------|
| "It's a one-line change, it's fine." | One-line changes break builds. Running the check costs seconds. |
| "Tests passed earlier." | Earlier was a different tree. Run them on this one. |
| "The diff looks correct." | Reading code is not running it. |
| "CI will catch it." | Then let CI's result be the evidence - don't claim done before it. |
| "I'm confident." | Confidence is not evidence. |
| "No time to run the full suite." | Then claim exactly what you verified, not "done". |

## Red flags - STOP

- "should work", "probably fine", "seems to pass".
- "Done!" / "Fixed!" typed before running anything.
- About to commit or hand off on the strength of a code read.
- Quoting a subagent's "it works" as your own verification.
