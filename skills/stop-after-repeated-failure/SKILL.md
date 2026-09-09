---
name: stop-after-repeated-failure
description: Use when the same specific task, fix, or command has failed three times in a row, or when you catch yourself looping over the same error with cosmetic variations - stop retrying and get direction.
type: Skill
title: Stop After Repeated Failure
status: draft
---

# Stop After Repeated Failure

## Overview

Three failed attempts at the *same* specific task means stop. Do not attempt a fourth 
blindly - it wastes tokens and rarely finds the cause.

## Trigger

- Same test still red after 3 distinct fix attempts.
- Same command failing the same way 3 times.
- Cycling through cosmetic variations of the same change.

## What to do instead

1. Stop editing.
2. Re-derive the root cause from first principles before touching code again: state a
   concrete hypothesis, find evidence that confirms or kills it, then act. A failure
   that repeats almost always means the cause is misidentified. Use a dedicated
   debugging skill for this step if the runtime provides one.
3. If still stuck, hand back to the user with:
   - the 3 attempts, one line each
   - the exact error each time
   - your current best hypothesis
   - the specific decision or piece of information you need from them.

## Rationalization table

| Excuse | Reality |
|--------|---------|
| "One more tweak and it's green." | You said that on attempt 2 and 3. The cause is misidentified. |
| "I'm so close." | Three identical failures is not close. It is the same wall. |
| "Stopping wastes the work so far." | Attempt 4 wastes more. The first 3 already told you the approach is wrong. |
| "The deadline means I can't stop." | The deadline changes the time budget, not the fact that you don't know the cause. |
| "Asking the user looks like giving up." | A crisp summary of 3 attempts + a hypothesis is progress, not surrender. |

## Red flags - STOP

- "One more small tweak will fix it."
- Re-running the same failing command hoping for a different result.
- Attempt 4 or beyond with no new hypothesis since attempt 1.
