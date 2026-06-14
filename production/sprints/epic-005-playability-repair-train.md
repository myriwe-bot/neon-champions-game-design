---
title: EPIC-005 Playability Repair Train
type: sprint-plan
status: approved
phase: production
owner: shared
created: 2026-06-13
updated: 2026-06-14
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

Approved direction after human playtest rejected EPIC-005 closeout on 2026-06-13. Run one story at a time. `STORY-QA-006`, `STORY-QA-007`, and `STORY-CMD-005` are DONE / merged. Human approved `STORY-STRAT-OBJECTIVE-001` Option 1 on 2026-06-14; it is the current READY implementation packet.

## Human closeout verdict

REJECT CLOSEOUT. The implementation works technically, but the player-facing loop is not yet readable enough to judge the intended Champion command / strategic-to-tactical fantasy.

## Ordered repair train

| Order | Story | Status | Purpose |
| ---: | --- | --- | --- |
| 1 | [STORY-QA-006 Strategic and Tactical State/Action Feedback Readability Pass](../stories/story-qa-006-strategic-tactical-state-action-feedback-readability-pass.md) | DONE / merged | PR #44; current actor, clickable actions, denial reasons, results, and target clarity across strategic/tactical modes. |
| 2 | [STORY-QA-007 Champion Encounter Initiation Clarity](../stories/story-qa-007-champion-encounter-initiation-clarity.md) | DONE / merged | PR #45; clarified Champion-vs-Champion engagement affordance, denial, enemy inspection, and tactical handoff. |
| 3 | [STORY-CMD-005 Champion Command Explanation Pass](../stories/story-cmd-005-champion-command-explanation-pass.md) | DONE / merged | PR #46; explained Rally/Drone and Marshal/Operator identity without changing command mechanics. |
| 4 | [STORY-STRAT-OBJECTIVE-001 Multi-Turn Objective Contest Direction](../stories/story-strat-objective-001-multi-turn-objective-contest-direction.md) | READY / approved | Implement narrow two-turn central-objective hold countdown; current Codex implementation packet. |

## Operating rule

Do not broaden completed repair stories into objective redesign. Objective capture changes are limited to the human-approved Option 1 two-turn countdown in `STORY-STRAT-OBJECTIVE-001`; defense waves and control-points remain out of scope.
