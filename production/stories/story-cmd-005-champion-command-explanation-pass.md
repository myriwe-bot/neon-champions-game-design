---
title: STORY-CMD-005 Champion Command Explanation Pass
type: story
status: ready-candidate
phase: production
owner: shared
created: 2026-06-13
updated: 2026-06-13
source_lore: []
related:
  [
    production/epics/epic-vslice-mvp-005-champion-command-and-operations-on-ramp,
    production/stories/story-cmd-004-tactical-command-usability-and-targeting-pass,
    production/stories/story-qa-006-strategic-tactical-state-action-feedback-readability-pass,
    design/gdd/tactical-combat/champion-operations-and-progression,
    docs/architecture/control-manifest,
  ]
approval: pending
---

# STORY-CMD-005 Champion Command Explanation Pass

## Status

READY-candidate / approval pending after `STORY-QA-006`. Human playtest showed that Rally Order and Drone Strike are visible but not understood. QA-006 may cover enough explanation; this candidate should be implemented only if command readability remains a blocker after QA-006.

## Human playtest source

The player reported:

- Rally Order availability is visible, but what it does is unclear.
- Rally Order denial/result is not understood.
- Drone Strike availability is visible, but what it does and target meaning are unclear.
- Second-use denial is not understood.
- Rally Order and Drone Strike do not yet feel differentiated.
- Marshal vs Operator identity is not yet clear.

## Player/design value

Make the two existing prototype commands read as Champion command identities rather than unexplained buttons.

## Scope candidate

- Add concise tactical command descriptions and examples for Rally Order and Drone Strike.
- Make Marshal vs Operator profile identity legible in the current tactical HUD.
- Improve command result/denial wording without changing mechanics.
- Show cost, target, one-use/major-slot limits, and current Command state in a compact way.

## Non-goals

- No new command effects.
- No balance change.
- No new Command economy/cooldowns/regeneration.
- No full Operations UI/spellbook.
- No final command names/lore/VFX/audio.

## Candidate acceptance

- A player can explain what Rally Order does, when it works, what it costs, and why it may be denied.
- A player can explain what Drone Strike does, who it will hit, what it costs, and why a second use may be denied.
- Marshal and Operator profile labels convey different command identities at prototype level.
