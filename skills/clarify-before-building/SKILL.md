---
name: clarify-before-building
description: Use before starting a new feature, changing architecture or a public interface, or acting on a request with more than one reasonable interpretation - surfaces the objective and the verification criteria first.
type: Skill
title: Clarify Before Building
status: draft
---

# Clarify Before Building

## Overview

For non-trivial or ambiguous work, get two things explicit before writing code:

1. **Objective** - the primary outcome the user actually wants.
2. **Verification** - the concrete test or acceptance criteria that will prove it is done.

If both are already clear from the request, the code, or a sensible default, skip this and proceed. This is not a license to re-ask settled questions or re-litigate a decision the user already made.

## When to use

- New feature or component.
- Changing architecture, data model, or a public interface.
- The request has more than one reasonable interpretation.

## When NOT to use

- Small, well-specified changes.
- Bug fixes with a clear reproduction.
- Anything where a sensible default is obvious and cheap to revise later.

## How

Ask targeted, closed questions - not "tell me more":

- "Goal: is this to cut p99 latency or to cut cost? They lead to different designs."
- "How do we verify success - a benchmark, a specific test, or a manual check?"

This skill is about *how* to build something already decided. If the open question is *what* to build at all, do that exploration first (use a dedicated brainstorming or discovery skill if the runtime provides one).

## Red flags

- About to scaffold files while unsure which of two interpretations is meant.
- No stated definition of "done" for a feature-sized task.
- Guessing at an interface other code will depend on.
