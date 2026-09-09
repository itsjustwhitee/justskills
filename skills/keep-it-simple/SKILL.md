---
name: keep-it-simple
description: Use before writing or refactoring any code - keeps the solution minimal (YAGNI, KISS) and comments scarce.
type: Skill
title: Keep It Simple
status: draft
---

# Keep It Simple

## Overview

Build the smallest thing that solves the task in front of you. Add structure when
a real need forces it, not in anticipation.

## Rules

- **YAGNI.** No config, abstraction, parameter, or hook for a case that is not
  here yet. Delete speculative code paths.
- **KISS.** Prefer the obvious implementation. A clever one-liner that needs a
  comment to parse is worse than three plain lines.
- **Match the surroundings.** New code reads like the code next to it - same
  naming, same idioms, same file layout.
- **Fewest moving parts.** One function beats two if the second has a single
  caller. A dependency you already have beats a new one.

## Comments

- Default to zero. Code shows *what*; a comment is only for a *why* the code
  cannot show - a hidden constraint, a workaround, a gotcha.
- If one is truly needed, a single short line. Never a multi-line block or a
  docstring restating the signature.
- Delete commented-out code and stale TODOs.

## Red flags

- "This might be useful later."
- An interface with one implementation and one caller.
- A comment that narrates the next line.
