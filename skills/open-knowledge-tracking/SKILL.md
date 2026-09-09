---
name: open-knowledge-tracking
description: Use after making an architectural decision, reversing one, resolving a non-trivial bug, or discovering a surprising constraint or workaround - records it in the project's docs/knowledge/ OKF bundle.
type: Skill
title: Open Knowledge Tracking
status: stable
---

# Open Knowledge Tracking

## Overview

Durable engineering knowledge lives under `docs/knowledge/` as an **Open Knowledge
Format (OKF) bundle**, following whatever version the spec currently defines:
<https://github.com/GoogleCloudPlatform/knowledge-catalog/blob/main/okf/SPEC.md>.

One markdown file per concept, grouped into topic subdirectories:

```
docs/knowledge/
  index.md                          optional listing        (reserved name)
  log.md                            history, newest first   (reserved name)
  auth/
    token-refresh-race.md
  database/
    connection-pool-exhaustion.md
```

## When to write a concept

- An architectural or design choice was made, or an earlier one reversed.
- A bug took more than a quick obvious fix to resolve.
- A non-obvious constraint, gotcha, or workaround was discovered.

Skip anything already obvious from the code or git history.

## Concept file

`type` is the only required frontmatter key. Use `Decision`, `Incident`, or
`Constraint`. Add `title`, `description`, `tags`, and `status`
(`draft | stable | deprecated`) when useful.

```markdown
---
type: Incident
title: Token refresh race on concurrent requests
description: Parallel requests each refreshed the token, invalidating the others.
tags: [auth, concurrency]
status: stable
generated: { by: "claude-code/claude-sonnet-5", at: 2026-09-09T10:00:00Z }
---

- **Symptom:** what was observed
- **Cause:** the underlying reason
- **Solution:** what was changed
- **Reasoning:** why this option over the alternatives considered
```

Actor strings for `generated` / `verified`: `human:<id>`, `<producer>/<version>`,
or `process:<id>`.

## log.md

Newest first, ISO date headings:

```markdown
# Knowledge Update Log

## 2026-09-09
* **Add**: [/auth/token-refresh-race.md](/auth/token-refresh-race.md) - fixed with a refresh mutex.
```

## Rules

- Append; do not rewrite a past concept. Supersede it: set the old file's
  `status: deprecated` and link to the replacement with a bundle-relative path
  (`/database/new-pooling.md`).
- Never paste secrets, tokens, credentials, or full environment variables.
- Write the concept file and its `log.md` line in the same change as the fix or
  decision, not "later".
