# justskills

A small, runtime-agnostic pack of agent skills. Each skill is a directory with a
`SKILL.md` carrying `name` + `description` frontmatter, the format understood by
Claude Code, Codex, Copilot CLI, Gemini CLI, and other AgentSkills-compatible
runtimes.

## Layout

```
.claude-plugin/plugin.json     manifest for loading as a Claude Code plugin
LICENSE                        MIT
skills/                        OKF bundle root
  index.md                     bundle listing (OKF)
  log.md                       update history (OKF)
  keep-it-simple/              minimal solution + scarce comments             (draft)
  safe-git/                    confirm before git writes, protect main
  no-secrets-in-output/        keep keys/tokens/env values out of output
  conventional-commits/        commit message format + emoji
  open-knowledge-tracking/     docs/knowledge/ decision & incident log
  clarify-before-building/     objective + verification before feature work   (draft)
  stop-after-repeated-failure/ 3-strikes rule                                 (draft)
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

- **All behaviour is a skill.** There is no always-on rules file. Broad defaults
  (`keep-it-simple`, `safe-git`, `no-secrets-in-output`) are skills with wide
  triggering descriptions, so a runtime that loads skills by `description` match
  still picks them up for the situations they cover.
- **Runtime-agnostic.** No skill references a runtime-specific built-in. Where a
  handoff helps (discovery before building, structured debugging), the text says
  "use a dedicated skill if the runtime provides one" rather than naming one.
- **No conflicts.** `clarify-before-building` is scoped to feature/architecture
  work and explicitly does not re-ask settled questions, so it does not fight an
  "act when you have enough info" default.
- **Each SKILL.md** has `name` + `description` frontmatter, the description starts
  with "Use when", and every skill stays well under 500 words.
- **Dual format.** Each `SKILL.md` also carries `type: Skill` / `title` / `status`,
  and `skills/` has an `index.md` + `log.md`, so the directory is simultaneously a
  valid AgentSkills pack and a valid [OKF](https://github.com/GoogleCloudPlatform/knowledge-catalog/blob/main/okf/SPEC.md)
  bundle. No OKF version is pinned - follow whatever the spec currently defines.
  Both specs ignore each other's extra frontmatter keys.
- **Testing status.** `conventional-commits` and `open-knowledge-tracking` pass
  application tests. `keep-it-simple`, `clarify-before-building`, and
  `stop-after-repeated-failure` are `status: draft` until they pass subagent
  pressure tests. `safe-git` and `no-secrets-in-output` are plain prohibitions
  and ship as `stable`.
