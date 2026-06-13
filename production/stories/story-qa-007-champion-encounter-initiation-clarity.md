---
title: STORY-QA-007 Champion Encounter Initiation Clarity
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
    production/stories/story-qa-006-strategic-tactical-state-action-feedback-readability-pass,
    production/stories/story-tac-008-champion-vs-champion-tactical-encounter-path,
    design/gdd/strategic-map,
    docs/architecture/control-manifest,
  ]
approval: pending
---

# STORY-QA-007 Champion Encounter Initiation Clarity

## Status

READY-candidate / approval pending after `STORY-QA-006`. Human approved the direction as part of the playability repair train, but this story should not become the current Codex implementation packet until QA-006 is merged and reviewed.

## Human playtest source

The player reported that Champion-vs-Champion combat is confusing: when Champions appear to be in the same area, battle does not trigger; movement may be blocked or the other Champion may become selected instead.

## Player/design value

Make Champion encounter initiation explicit so the player understands whether they can engage, cannot enter, or are selecting another Champion.

## Scope candidate

- Clarify same-node / adjacent / contested-node Champion encounter rules in current prototype terms.
- Add explicit player-facing affordance or denial text for Champion encounter initiation.
- Prevent “enemy selected instead of engagement understood” confusion.
- Preserve existing battle setup/result mechanics unless a narrow approved rule clarification is required.

## Non-goals

- No new strategic AI.
- No fog/ambush/stealth rules.
- No multi-Champion battles.
- No full diplomacy/zone-of-control system.
- No final map redesign.

## Candidate acceptance

- The player can tell when an enemy Champion is engageable.
- The player can tell why a Champion cannot move into or through an occupied/contested location.
- Clicking/selecting enemy-related UI cannot be mistaken for taking control of the enemy Champion.
- Champion-vs-Champion battle launch remains covered by PlayMode smoke/evidence.
