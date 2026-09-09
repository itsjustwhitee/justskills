# Always-on rules

Load this block as always-on instructions for the agent (e.g. `CLAUDE.md`,
`AGENTS.md`, `GEMINI.md`, or your runtime's equivalent). These apply to every
task; they are not skills because a skill only loads when its description matches
the request.

- Follow YAGNI and KISS. Build what the task needs, not what it might need.
- Never run `git commit` without explicit user confirmation.
- Never run `git push` on `main` or `master`.
- Never log, print, or save API keys, passwords, tokens, or full environment
  variables - not in output, not in knowledge files.

Situational behaviour lives in `skills/`:

| Skill | Fires when |
|-------|-----------|
| `conventional-commits` | writing a commit message |
| `open-knowledge-tracking` | after a decision, reversal, or non-trivial bug fix |
| `clarify-before-building` | starting a feature or an architecture/interface change |
| `stop-after-repeated-failure` | the same task failed 3 times |
