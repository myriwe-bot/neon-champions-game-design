---
title: EPIC-005 Playability Repair Train
type: sprint-plan
status: approved
phase: production
owner: shared
created: 2026-06-13
updated: 2026-06-13
source_lore: []
related:
  [
    production/epics/epic-vslice-mvp-005-champion-command-and-operations-on-ramp,
    production/stories/story-qa-006-strategic-tactical-state-action-feedback-readability-pass,
    production/stories/story-qa-007-champion-encounter-initiation-clarity,
    production/stories/story-cmd-005-champion-command-explanation-pass,
    production/stories/story-strat-objective-001-multi-turn-objective-contest-direction,
  ]
approval: approved
---

# EPIC-005 Playability Repair Train

## Status

Approved direction after human playtest rejected EPIC-005 closeout on 2026-06-13. Run one story at a time. `STORY-QA-006` is DONE / merged. `STORY-QA-007` is the current READY implementation packet.

## Human closeout verdict

REJECT CLOSEOUT. The implementation works technically, but the player-facing loop is not yet readable enough to judge the intended Champion command / strategic-to-tactical fantasy.

## Ordered repair train

| Order | Story | Status | Purpose |
| ---: | --- | --- | --- |
| 1 | [STORY-QA-006 Strategic and Tactical State/Action Feedback Readability Pass](../stories/story-qa-006-strategic-tactical-state-action-feedback-readability-pass.md) | DONE / merged | PR #44; current actor, clickable actions, denial reasons, results, and target clarity across strategic/tactical modes. |
| 2 | [STORY-QA-007 Champion Encounter Initiation Clarity](../stories/story-qa-007-champion-encounter-initiation-clarity.md) | READY / approved | Current implementation packet: clarify how Champion-vs-Champion encounters start or why movement/engagement is denied. |
| 3 | [STORY-CMD-005 Champion Command Explanation Pass](../stories/story-cmd-005-champion-command-explanation-pass.md) | READY-candidate | If still needed after QA-006, make Rally/Drone and Marshal/Operator identity understandable. |
| 4 | [STORY-STRAT-OBJECTIVE-001 Multi-Turn Objective Contest Direction](../stories/story-strat-objective-001-multi-turn-objective-contest-direction.md) | DRAFT | Design heavier objective-contest/capture direction; not current Codex work. |

## Operating rule

Do not broaden QA-006 into the later stories. If QA-006 reveals that encounter rules, command design, or objective capture rules must change, stop and prepare the next story rather than expanding scope.
