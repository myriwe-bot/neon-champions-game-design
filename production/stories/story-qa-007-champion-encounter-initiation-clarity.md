---
title: STORY-QA-007 Champion Encounter Initiation Clarity
type: story
status: ready
phase: production
owner: shared
created: 2026-06-13
updated: 2026-06-13
source_lore: []
related:
  [
    production/epics/epic-vslice-mvp-005-champion-command-and-operations-on-ramp,
    production/sprints/epic-005-playability-repair-train,
    production/stories/story-qa-006-strategic-tactical-state-action-feedback-readability-pass,
    production/stories/story-tac-008-champion-vs-champion-tactical-encounter-path,
    design/gdd/strategic-map,
    docs/architecture/control-manifest,
    docs/architecture/testing-strategy,
    docs/architecture/ci-build-automation,
  ]
approval: approved
---

# STORY-QA-007 Champion Encounter Initiation Clarity

## Status

READY / approved for Codex implementation. `STORY-QA-006` is DONE / merged, and this is the next approved narrow playability repair from the human playtest train.

## Human playtest source

The player reported that Champion-vs-Champion combat is confusing:

- When Champions appear to be in the same area, battle does not trigger.
- Movement may be blocked without clear explanation.
- Clicking or interacting near the other Champion may make it feel like the other Champion was selected instead of engaged.
- The player cannot tell whether an enemy Champion is engageable, blocking, occupying a route/node, or simply another marker on the map.

Preserve this complaint as first-class acceptance authority. Do not dilute it into generic “improve UX”.

## Player/design value

Make Champion encounter initiation explicit so the player understands whether they can engage, cannot enter, or are selecting/inspecting another Champion. This should make the strategic-to-tactical Champion battle path judgeable without changing the underlying encounter design.

## Implementation scope

One narrow Champion encounter clarity pass:

- Surface enemy Champion encounter state in the strategic snapshot/HUD/panels using current prototype rules.
- Show when an enemy Champion is engageable by the selected active Champion.
- Show an explicit player-facing Champion encounter affordance/control when the existing rules allow launching the encounter.
- Show clear denial text when movement/engagement is not allowed because of faction, active Champion, reachability, defeated status, location, or other existing validation.
- Make enemy Champion markers/text/buttons visually/textually distinct from selectable friendly Champions.
- Prevent enemy Champion UI from looking like it selects or transfers control of the enemy Champion.
- Keep the existing ChampionEncounterService / BattleSetup / tactical handoff semantics unless a tiny presentation-layer adapter is needed to expose current validation state.
- Add PlayMode smoke/evidence showing the pre-engagement state, a clear encounter affordance/denial, and successful Champion-vs-Champion launch.

## Out of scope

- No new strategic AI.
- No fog, ambush, stealth, hidden-information, diplomacy, zone-of-control, or overwatch rules.
- No multi-Champion battles.
- No map redesign away from the current node graph.
- No objective/capture rule changes.
- No new battle mechanics, command effects, units, attack types, creature depth, balance, final art, icons, VFX, audio, animation, portraits, or lore copy.
- No save/load or persistence expansion.
- No broad rewrite of Champion movement/pathfinding. If the current rules are contradictory and cannot be explained without rule changes, stop and report the exact contradiction instead of expanding scope.

## Acceptance criteria

- Given the selected active Champion can launch an existing Champion-vs-Champion encounter, the strategic UI shows an explicit “Engage Champion”/equivalent affordance naming the enemy Champion.
- Given an enemy Champion is present but not engageable, the strategic UI explains why in player-facing terms instead of silently blocking movement or appearing to select the enemy.
- Given the player clicks/interacts with enemy Champion-related UI, feedback cannot be mistaken for taking control of the enemy Champion.
- Given Champion encounter launch succeeds, feedback names attacker, defender, source node/location, and that tactical Champion battle mode launched.
- Given Champion encounter launch is denied, feedback names the reason and does not mutate strategic/tactical state.
- Existing ChampionEncounterService battle setup/result mechanics remain unchanged unless the story records a stop-condition and receives explicit follow-up approval.
- Existing QA-006 state/action feedback remains visible and is not regressed.
- PlayMode smoke evidence captures: enemy Champion encounter affordance/clarity, denied or non-engageable state if applicable, and successful Champion-vs-Champion tactical launch.
- `git diff --check`, relevant EditMode tests, relevant PlayMode smoke tests, and Unity Foundation CI exact-head pass before merge.

## Suggested implementation branch

`story/STORY-QA-007-champion-encounter-initiation-clarity`

## Suggested PR title

`STORY-QA-007 Champion encounter initiation clarity`

## Ambiguity check

Status: PASS.

Human-approved implementation constraints:

- This is a clarity/affordance repair, not a new encounter rules story.
- Preserve the user's exact complaint: moving into the same area does not clearly trigger battle; movement may be blocked; enemy Champion interaction can feel like selecting the other Champion.
- May add prototype-safe text, colors, panels, markers, buttons, snapshots, validation previews, denial summaries, and PlayMode coverage.
- Must not add new map structure, objective rules, Champion battle mechanics, strategic AI, fog/stealth, zone-of-control, final art/content, or save/load.
- If implementation needs a gameplay rule change to make the experience coherent, stop and report the rule-change need instead of expanding scope.

## Evidence requirements

Create or update `production/evidence/STORY-QA-007/README.md` in the Unity repo and include PNG evidence for at least:

1. Strategic state where the selected active Champion can see an enemy Champion encounter affordance or clear non-engageable explanation.
2. Enemy Champion UI/marker/panel clarity proving enemy interaction is not confused with friendly Champion selection.
3. Champion encounter launch feedback naming attacker/defender/location.
4. Tactical Champion battle handoff after successful launch.

README must include tests run, CI URL, omissions/deferred work, and confirmation that encounter mechanics/rules were not expanded.
