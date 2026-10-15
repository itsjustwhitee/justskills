---
name: task-knowledge-organize
description: Use when a finding is tied to a tracked task/ticket that spans repos, demo environments, or no repo at all - records it under ~/knowledge/<TASK-ID>/(/<subtask>)* as an OKF bundle (subtasks nest recursively to whatever level is atomic), cross-linked to other tasks by topic instead of being scoped to one repo's docs/knowledge/.
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

A task folder can itself contain subtask folders, recursively, as deep as the
tracked work is actually broken down - a task's subtasks may have their own
subtasks, down to whatever level is logically atomic there. A folder is a
**leaf** once it holds only concept files (no further subtask folders):

```
~/knowledge/
  index.md                     global, cross-task topic index   (reserved name)
  PO-5/
    index.md                    listing: subtasks + concepts     (reserved name)
    log.md                       history, newest first            (reserved name)
    two-dag-split.md
    onnx-to-rvc4/                subtask folder (same shape, recursively)
      index.md
      log.md
      quantization-knn.md
      bitwidth-sweep/            sub-subtask folder, still growable
        index.md
        log.md
        act-bitwidth-vit-degradation.md
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
Incident | Constraint`, same frontmatter, same body shape. The folder path
**is** the task/subtask context, so do not duplicate the task ID inside the
frontmatter.

**Default to flat.** Do not pre-create subtask folders speculatively. Nest
only when the parent either (a) already tracks that subtask as a distinct
unit (e.g. a ticket subtask/sub-issue), or (b) is accumulating enough concept
files that a natural sub-grouping has emerged. One concept file belongs
directly in its nearest existing folder, not in a new single-item subfolder
created just for it.

## Every folder's `index.md`

One line per **direct child** - subtask folders first, then concept files,
same shape as a skill-pack index. Do not list grandchildren; each folder's
`index.md` only describes what's directly inside it:

```markdown
# PO-5 knowledge

## Subtasks
* [onnx-to-rvc4](/onnx-to-rvc4/index.md) - SNPE quantization + graph-prepare

## Concepts
* [Two-DAG split](/two-dag-split.md) - miniad-to-onnx / onnx-to-rvc4 contract
```

## Every folder's `log.md`

Same format as `open-knowledge-tracking`'s `log.md`: newest first, ISO date
headings. Record an entry at the level (task or subtask folder) where the
concept file actually lives - do not bubble entries up to parent logs.

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
* [PO-5/onnx-to-rvc4/quantization-knn.md](/PO-5/onnx-to-rvc4/quantization-knn.md)

### Docktor / blueprint
* [PO-5/two-dag-split.md](/PO-5/two-dag-split.md)
* [PIZ163/...]
```

This file is maintained by hand, not generated - append a line under the
relevant topic heading only when a concept is genuinely useful outside its
own task folder.

## Determining where a concept belongs

Never guess a ticket prefix/number or a subtask breakdown. Walk down from
`~/knowledge/<TASK-ID>/` following existing subtask folders to the most
specific one that already matches the work; if none fits and the finding
doesn't warrant a new subtask folder (see "Default to flat" above), it
belongs in the nearest existing folder up the chain. Ask the user before
creating a new top-level task folder, and before creating a new subtask
folder if it's not obvious the subtask is already tracked elsewhere.

## Rules

- Same append-only/supersede rules as `open-knowledge-tracking`: never rewrite
  a past concept's substance, supersede it instead.
- Write the concept file and its folder's `log.md` line in the same change.
  If the concept is relevant beyond its own task/subtask, also add it to the
  root `~/knowledge/index.md` topic section in that same change - the global
  topic index only ever lives at the root, never at an intermediate level.
- Never paste secrets, tokens, credentials, or full environment variables.
