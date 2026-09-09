# justskills

A small pack of agent skills plus a set of always-on rules. Runtime-agnostic:
each skill is a directory with a `SKILL.md` carrying `name` + `description`
frontmatter, the format understood by Claude Code, Codex, Copilot CLI, Gemini
CLI, and other AgentSkills-compatible runtimes.

## Layout

```
general.md                     always-on rules to load as agent instructions
.claude-plugin/plugin.json     manifest for loading as a Claude Code plugin
LICENSE                        MIT
skills/                        OKF bundle root
  index.md                     bundle listing (OKF)
  log.md                       update history (OKF)
  conventional-commits/        commit message format + emoji
  open-knowledge-tracking/     docs/knowledge/ decision & error log
  clarify-before-building/     objective + verification before feature work  (draft)
  stop-after-repeated-failure/ 3-strikes rule                                (draft)
```

## Install

Copy the skills into a directory your agent scans:

```
cp -r skills/* ~/.agents/skills/     # cross-runtime alias (Codex, Copilot, Gemini)
cp -r skills/* ~/.claude/skills/     # Claude Code
```

On Claude Code, load the whole repo as a plugin - `.claude-plugin/plugin.json` is
included and skills are auto-discovered from `skills/`. Project-scoped: drop
`skills/` into the repo where the runtime looks for local skills.

It can also be added through a skills manager (e.g. `skillsmanager`) by pointing it
at this repo, so the pack is installed, updated, and enabled/disabled from one
place instead of copying files by hand.

## Design notes

- **Runtime-agnostic.** No skill references a runtime-specific built-in. Where a
  handoff helps (discovery before building, structured debugging), the text says
  "use a dedicated skill if the runtime provides one" rather than naming one.
- **No conflicts.** `clarify-before-building` is scoped to feature/architecture
  work and explicitly does not re-ask settled questions, so it does not fight an
  "act when you have enough info" default.
- **Always-on vs situational.** Guardrails that must always hold (no auto-commit,
  protected main, no secrets in output, YAGNI/KISS) stay in `general.md`, because
  a skill only loads when its `description` matches the current request.
- **Each SKILL.md** has `name` + `description` frontmatter, the description starts
  with "Use when", and every skill stays well under 500 words.
- **Dual format.** Each `SKILL.md` also carries `type: Skill` / `title` / `status`,
  and `skills/` has an `index.md` + `log.md`, so the directory is simultaneously a
  valid AgentSkills pack and a valid [OKF](https://github.com/GoogleCloudPlatform/knowledge-catalog/blob/main/okf/SPEC.md)
  bundle. No OKF version is pinned - follow whatever the spec currently defines.
  Both specs ignore each other's extra frontmatter keys.
- **Testing status.** `conventional-commits` and `open-knowledge-tracking` are
  reference skills and marked `status: stable`. The two discipline skills
  (`clarify-before-building`, `stop-after-repeated-failure`) are `status: draft`
  until run through subagent pressure tests. No `verified` provenance block is
  set on any of them yet.
