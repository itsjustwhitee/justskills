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
  decisions/
    0001-single-shared-pg-pool.md
  database/
    connection-pool-exhaustion.md
```

## When to write a concept

- An architectural or design choice was made, or an earlier one reversed.
- A bug took more than a quick obvious fix to resolve.
- A non-obvious constraint, gotcha, or workaround was discovered.

Skip anything already obvious from the code or git history.

## Concept file

`type` is the only required frontmatter key. Add `title`, `description`, `tags`
when useful. Actor strings for `generated` / `verified`: `human:<id>`,
`<producer>/<version>`, or `process:<id>`.

### type: Incident - a bug that took real work

```markdown
---
type: Incident
title: Token refresh race on concurrent requests
tags: [auth, concurrency]
status: stable
---

- **Symptom:** what was observed
- **Cause:** the underlying reason
- **Solution:** what was changed
- **Reasoning:** why this option over the alternatives considered
```

Provenance fields (`generated`, `verified`) are optional; omit them unless the project asks for them.

### type: Decision - an architectural choice (Nygard ADR)

Number these: `docs/knowledge/decisions/0001-<slug>.md`, `0002-...`. Lifecycle
`status: proposed | accepted | superseded` (ADR values; OKF tolerates them).

```markdown
---
type: Decision
title: Use a single shared Postgres pool
tags: [database]
status: accepted
generated: { by: "human:matteo", at: 2026-09-09T10:00:00Z }
---

- **Context:** what forces a choice now - constraints and pressures.
- **Decision:** what we are doing.
- **Consequences:** what gets easier, what gets harder, what we accept.
- **Alternatives:** each option rejected, and why.
```

## log.md

Newest first, ISO date headings:

```markdown
# Knowledge Update Log

## 2026-09-09
* **Add**: [/decisions/0001-single-shared-pg-pool.md](/decisions/0001-single-shared-pg-pool.md) - one process-wide pool.
```

## Rules

- Append; do not rewrite a past concept's substance.
- **Superseding an Incident/Constraint:** set the old file's `status: deprecated`
  and link the replacement with a bundle-relative path (`/database/new-pooling.md`).
- **Superseding a Decision:** keep the old file, set `status: superseded`, add a
  `superseded_by: /decisions/0007-<slug>.md` line. Never edit an accepted
  Decision's substance - write a new numbered one.
- Never paste secrets, tokens, credentials, or full environment variables.
- Write the concept file and its `log.md` line in the same change as the fix or
  decision, not "later".
