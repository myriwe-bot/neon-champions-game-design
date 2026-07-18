---
title: EPIC-018 Player Entry and Physical Map Recovery Train
type: sprint-plan
status: active
phase: production
owner: shared
created: 2026-07-17
updated: 2026-07-18
approval: approved
related: [production/epics/epic-018-physical-adventure-map-and-player-entry-recovery, production/stories/story-standalone-entry-001-windows-player-entry-and-launch-smoke, production/stories/story-map-visual-slice-001-physical-arctic-adventure-map-and-shell, production/stories/story-champion-army-interaction-001-discoverable-champion-army-and-selection-continuity]
---

# EPIC-018 Player Entry and Physical Map Recovery Train

## Human verdict that opened the train

`STORY-PROTOTYPE-CONTINUITY-QA-001`: `BLOCKED / REJECT CLOSEOUT`.

The standalone executable did not reach the player shell. The Editor workaround exposed a map that was unreadable, unclear, and insufficiently interactive for the approved continuity route. Opponent movement after End Turn was visible, but usability blocked all further judgment.

## Ordered train

| Order | Packet | Status | Gate |
|---:|---|---|---|
| 1 | `STORY-STANDALONE-ENTRY-001` | DONE / merged / verified | Unity PR #170 merged; post-merge run 29609782110 passed build+launch, EditMode, PlayMode, and validator |
| 2 | `STORY-MAP-VISUAL-SLICE-001` | DONE / merged / post-merge verified | Final head `b4afc997…` received owner APPROVE; PR #172 merged as `0a704445…`; post-merge run `29663206375` passed |
| 3 | `STORY-CHAMPION-ARMY-INTERACTION-001` | READY / approved / awaiting Unity pointer activation | structured truthful army discovery and Champion -> base -> Champion context continuity; no inventory or stack-management expansion |
| 4 | Human continuity replaytest | DRAFT | launch, readability, Champion/base discovery, save/relaunch/Continue, and post-resume opponent pressure are all testable |

Orders 1 and 2 are closed. Order 3 is the sole approved next packet; implementation remains fail-closed until its Unity README pointer activation merges and passes post-merge CI.

## Direction lock

- Physical adventure map over hidden authored corridor graph.
- No visible polygon/node/graph metaphor in normal play.
- No full square/hex/free-movement rewrite in this train.
- One representative slice before full-map scaling.
- Preserve human complaint wording as acceptance authority.
- Human visual/playtest evidence outranks screenshot semantic assertions.

## Current prompt

`production/sprints/codex-story-champion-army-interaction-001.prompt.txt`

The packet exposes the real current Champion army as structured data-driven rows/cards and proves clean Champion -> base -> Champion context replacement through production pointer input. It may not invent inventory, equipment, stack rearrangement, new mechanics, topology, content, or full-map work.
