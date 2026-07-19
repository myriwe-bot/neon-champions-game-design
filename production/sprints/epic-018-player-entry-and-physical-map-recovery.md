---
title: EPIC-018 Player Entry and Physical Map Recovery Train
type: sprint-plan
status: active
phase: production
owner: shared
created: 2026-07-17
updated: 2026-07-19
approval: approved
related: [production/epics/epic-018-physical-adventure-map-and-player-entry-recovery, production/stories/story-standalone-entry-001-windows-player-entry-and-launch-smoke, production/stories/story-map-visual-slice-001-physical-arctic-adventure-map-and-shell, production/stories/story-champion-army-interaction-001-discoverable-champion-army-and-selection-continuity, production/stories/story-map-physical-rollout-001-complete-duel-map-and-two-faction-interaction-parity]
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
| 3 | `STORY-CHAMPION-ARMY-INTERACTION-001` | DONE / merged / verified | Unity PR #174 merged as `07aec855…`; post-merge run `29684259824` passed; structured truthful army discovery and Champion -> base -> Champion context continuity |
| 4 | `STORY-MAP-PHYSICAL-ROLLOUT-001` | READY / approved / pointer activation pending | Complete current ten-node/twelve-route physical duel map with HRC/QXZ normal-input and context parity |
| 5 | Human continuity replaytest | DRAFT | launch, complete-map readability, both-faction interaction, save/relaunch/Continue, and post-resume opponent pressure are all testable |

Orders 1–3 are closed. Order 4 is the sole next approved implementation packet and becomes runnable only after Unity pointer activation.

## Direction lock

- Physical adventure map over hidden authored corridor graph.
- No visible polygon/node/graph metaphor in normal play.
- No full square/hex/free-movement rewrite in this train.
- One representative slice before full-map scaling.
- Preserve human complaint wording as acceptance authority.
- Human visual/playtest evidence outranks screenshot semantic assertions.

## Current prompt

`production/sprints/codex-story-map-physical-rollout-001.prompt.txt`

The packet scales the approved physical Arctic map treatment across all current duel-map nodes/routes and both factions while preserving graph rules, scenario JSON, gameplay, save/AI/tactical behavior, and asset provenance. It may not become a topology rewrite, content expansion, final-art pass, or mechanics bundle.
