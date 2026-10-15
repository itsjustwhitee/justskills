---
name: task-knowledge-organize
description: Use when a finding is tied to a tracked task/ticket that spans repos, demo environments, or no repo at all - records it under ~/knowledge/<TASK-ID>/ as an OKF bundle, cross-linked to other tasks by topic instead of being scoped to one repo's docs/knowledge/.
type: Skill
title: Task Knowledge Organize
status: draft
---

# Task Knowledge Organize

## Overview

Builds on [open-knowledge-tracking](/open-knowledge-tracking/SKILL.md)'s OKF
concept format, but roots the bundle at `~/knowledge/` instead of inside a
single repo, and groups top-level by **tracked task/ticket ID** instead of by
topic. Use it when the knowledge:

- spans more than one repo (a task touches `edgeye-dags` and `miniad`),
- lives partly or entirely outside any repo (a blueprint authored only in a
  web UI, a decision made in a meeting/chat), or
- should stay discoverable by the task that produced it even after the work
  moves between repos.

If the knowledge is tightly scoped to one repo and useful mainly to people/
agents working in that repo, use `open-knowledge-tracking`'s repo-local
`docs/knowledge/` instead. The two are not mutually exclusive: a repo can
still keep its own `docs/knowledge/` for repo-internal concepts while
cross-repo or ticket-driven findings go here.

## Structure

```
~/knowledge/
  index.md               global, cross-task topic index   (reserved name)
  PO-5/
    index.md              per-task listing                (reserved name)
    log.md                 per-task history, newest first   (reserved name)
    two-dag-split.md
    quantization-knn.md
  PIZ160/
    index.md
    log.md
    ...
  PIZ163/
    index.md
    log.md
    ...
```

Concept files follow `open-knowledge-tracking` unchanged: `type: Decision |
Incident | Constraint`, same frontmatter, same body shape. The task folder
**is** the task context, so do not duplicate the task ID inside the
frontmatter.

## Per-task `index.md`

One line per concept file, same shape as a skill-pack index:

```markdown
# PO-5 knowledge

* [Two-DAG split](/two-dag-split.md) - miniad-to-onnx / onnx-to-rvc4 contract
* [Quantization kNN](/quantization-knn.md) - bitwidth sweep, calibration pitfalls
```

## Per-task `log.md`

Same format as `open-knowledge-tracking`'s `log.md`: newest first, ISO date
headings.

## Global `index.md`

Lists the task folders, and groups entries **by cross-cutting topic** so a
concept relevant to more than one task is discoverable from either angle:

```markdown
# Knowledge index

## Tasks
* [PO-5](/PO-5/index.md) - OAK-4D / RVC4 conversion PoC
* [PIZ160](/PIZ160/index.md) - RevPi
* [PIZ163](/PIZ163/index.md) - pizza detector cross-validation blueprint

## By topic
### Quantization
* [PO-5/quantization-knn.md](/PO-5/quantization-knn.md)

### Docktor / blueprint
* [PO-5/two-dag-split.md](/PO-5/two-dag-split.md)
* [PIZ163/...]
```

This file is maintained by hand, not generated - append a line under the
relevant topic heading only when a concept is genuinely useful outside its
own task folder.

## Determining the task ID

Never guess a ticket prefix/number. If it is not already stated in the
conversation, ask before creating a new task folder.

## Rules

- Same append-only/supersede rules as `open-knowledge-tracking`: never rewrite
  a past concept's substance, supersede it instead.
- Write the concept file, its task-local `log.md` line, and (if relevant
  beyond this task) the global `index.md` topic line in the same change.
- Never paste secrets, tokens, credentials, or full environment variables.
