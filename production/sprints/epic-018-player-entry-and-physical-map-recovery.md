---
title: EPIC-018 Player Entry and Physical Map Recovery Train
type: sprint-plan
status: active
phase: production
owner: shared
created: 2026-07-17
updated: 2026-07-17
approval: approved
related: [production/epics/epic-018-physical-adventure-map-and-player-entry-recovery, production/stories/story-standalone-entry-001-windows-player-entry-and-launch-smoke, production/stories/story-map-visual-slice-001-physical-arctic-adventure-map-and-shell]
---

# EPIC-018 Player Entry and Physical Map Recovery Train

## Human verdict that opened the train

`STORY-PROTOTYPE-CONTINUITY-QA-001`: `BLOCKED / REJECT CLOSEOUT`.

The standalone executable did not reach the player shell. The Editor workaround exposed a map that was unreadable, unclear, and insufficiently interactive for the approved continuity route. Opponent movement after End Turn was visible, but usability blocked all further judgment.

## Ordered train

| Order | Packet | Status | Gate |
|---:|---|---|---|
| 1 | `STORY-STANDALONE-ENTRY-001` | DONE / merged / verified | Unity PR #170 merged; post-merge run 29609782110 passed build+launch, EditMode, PlayMode, and validator |
| 2 | `STORY-MAP-VISUAL-SLICE-001` | READY / approved / pointer pending | exact HRC slice packet approved; Unity pointer activation, then human APPROVE/REVISE/REJECT on exact-head evidence |
| 3 | Champion/army/base interaction follow-up | DRAFT | formed from approved slice and exact remaining complaints |
| 4 | Human continuity replaytest | DRAFT | launch, readability, Champion/base discovery, save/relaunch/Continue, and post-resume opponent pressure are all testable |

Order 1 is closed. Order 2 is the sole next packet and becomes runnable only after verified Unity pointer activation. Do not form or parallelize order 3.

## Direction lock

- Physical adventure map over hidden authored corridor graph.
- No visible polygon/node/graph metaphor in normal play.
- No full square/hex/free-movement rewrite in this train.
- One representative slice before full-map scaling.
- Preserve human complaint wording as acceptance authority.
- Human visual/playtest evidence outranks screenshot semantic assertions.

## Current prompt

`production/sprints/codex-story-map-visual-slice-001.prompt.txt`

The map-slice prompt is approved but remains guarded until the Unity current-task pointer names it from the published design-control commit.
