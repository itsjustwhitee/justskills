---
name: conventional-commits
description: Use when writing a git commit message or preparing a commit - enforces Conventional Commits syntax with a leading gitmoji, and the no-commit-without-confirmation rule.
type: Skill
title: Conventional Commits
status: stable
---

# Conventional Commits

## Overview

Every commit message follows Conventional Commits, prefixed with one representative emoji.

Format: `<emoji> <type>(<scope>): <subject>`

- `type`: feat, fix, docs, style, refactor, perf, test, build, ci, chore, revert
- `scope`: optional, the affected area (e.g. `auth`, `api`)
- `subject`: imperative mood, lowercase, no trailing period, <= 50 chars

## Emoji by type

✨ feat · 🐛 fix · 📝 docs · 🎨 style · ♻️ refactor · ⚡️ perf · ✅ test · 📦 build · 👷 ci · 🔧 chore · ⏪️ revert

## Examples

- `✨ feat(auth): add token validation`
- `🐛 fix(api): resolve timeout crash`
- `♻️ refactor(parser): extract token scanner`

## Body and footer

- Blank line after the subject, then wrap the body at 72 columns and explain *why*, not *what*.
- Breaking change: footer line `BREAKING CHANGE: <description>`.
- Issue references go in the footer: `Refs: #123`.

## Guardrails

- Never run `git commit` without explicit user confirmation.
- Never `git push` to `main` or `master`.
- One logical change per commit - do not bundle unrelated edits.
