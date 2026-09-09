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
- **Look before you overwrite.** Read what a destructive command will discard
  (`reset`, `checkout -- .`, `clean -fd`) before running it.

## Red flags

- "I'll just commit this so it's saved."
- Force-pushing to get past a conflict instead of merging.
- `git checkout .` or `git clean` over unreviewed local changes.
