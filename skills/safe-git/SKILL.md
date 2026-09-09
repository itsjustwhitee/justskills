---
name: safe-git
description: Use before running any git command that writes - commit, push, reset, rebase, branch or tag deletion, force-push, or history rewrite.
type: Skill
title: Safe Git
status: stable
---

# Safe Git

## Overview

Git write operations are confirmed with the user first, and shared history is
never rewritten unless the user asks for that specific action.

## Rules

- **No autonomous commit.** Never `git commit` unless the user asked for it in
  this session. Staging and showing a diff is fine; committing is not.
- **Protect the main line.** Never `git push` to `main` or `master` on your own
  initiative. Push feature branches and let the user merge.
- **No rewrite without a request.** `git push --force` / `--force-with-lease`,
  `git reset --hard`, `git rebase`, amending pushed commits, branch or tag
  deletion - only when the user explicitly asks for that action.
- **Work on a branch.** If asked to commit while on `main` or `master`, create a
  branch first.
- **Green before integrate.** Run the full test suite on the exact tree being
  merged or PR'd. Integrate only on a clean run.
- **Confirm the base branch.** Before a merge, state which branch you are merging
  into and get a yes. A wrong merge is expensive to undo.
- **Typed confirmation for the irreversible.** For history rewrite, hard reset, 
  force-push, or branch/worktree deletion, show exactly what will be lost and 
  require the user to type the word `discard` (or the branch name). "ok" / "go" is
  not enough.
- **Look before you overwrite.** Read what a destructive command will discard
  (`reset`, `checkout -- .`, `clean -fd`) before running it.

## Rationalization table

| Excuse | Reality |
|--------|---------|
| "I'll just commit so the work is saved." | Staging saves it for review. Commit is the user's call. |
| "Force-push is faster than fixing the conflict." | It also silently drops their commits. Merge. |
| "They said 'go' earlier." | Earlier approval was for that step, not this irreversible one. |
| "The branch is obviously stale, I'll delete it." | Obvious to you. Show it, ask, let them type the confirmation. |
| "Tests are slow, the change is trivial." | Then it will pass fast. Run it before you integrate. |

## Red flags - STOP

- "I'll just commit this so it's saved."
- Force-pushing to get past a conflict instead of merging.
- `git checkout .` or `git clean` over unreviewed local changes.
- Merging without having said the target branch out loud.
- Running a destructive command on "ok" instead of a typed confirmation.
