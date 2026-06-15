---
title: STORY-STRAT-OBJECTIVE-001 Multi-Turn Objective Contest Direction
type: story
status: done
phase: production
owner: shared
created: 2026-06-13
updated: 2026-06-15
source_lore: []
related:
  [
    design/gdd/strategic-map,
    production/epics/epic-vslice-mvp-005-champion-command-and-operations-on-ramp,
    production/sprints/epic-005-playability-repair-train,
    production/stories/story-obj-001-scenario-objective-state-and-victory-feedback,
    production/stories/story-obj-002-guarded-site-defender-strength-tiers,
    production/stories/story-loop-004-objective-champion-combat-and-casualty-stakes-smoke,
    production/stories/story-cmd-005-champion-command-explanation-pass,
    docs/architecture/control-manifest,
    docs/architecture/testing-strategy,
    docs/architecture/ci-build-automation,
  ]
approval: approved
---

# STORY-STRAT-OBJECTIVE-001 Multi-Turn Objective Contest Direction

## Status

DONE / merged. Unity PR #47 merged as `2eab67d8a10824a122493271feae94d53119c440`; post-merge Unity Foundation CI passed: https://github.com/myriwe-bot/neon-champions-unity/actions/runs/27530718158

Human approval recorded on 2026-06-14: approve the recommended **Option 1 — narrow two-turn capture countdown**. This story may change central-objective victory timing from same-interaction/sneak capture toward the already-approved Strategic Map §13 hold-progress contract.

`STORY-CMD-005` is DONE / merged. This is the next approved Unity implementation story.

## Human playtest source

The player reported:

- Objective capture is too easy.
- It is possible to “sneak” the objective.
- In the real game, capture should likely take several turns and possibly several rounds of defenses.
- Guarded vs unguarded state is unclear.

Preserve this complaint as first-class design authority. Do not turn it into generic “make objective harder”.

## Approved implementation shape

Implement the smallest real rule change: a visible two-turn central-objective hold countdown.

Authoritative rule shape:

1. Interacting with / claiming the central objective starts or confirms objective control/hold state for the acting faction; it must not silently win the scenario in the same interaction.
2. The same faction must still control the central objective at a later own-turn objective check before objective victory resolves.
3. The working default is Strategic Map §13’s approved value: `objectiveHoldRequired = 2` consecutive own-turn checks.
4. Scenario definitions/state should store the required count rather than hardcoding victory to an immediate capture.
5. Objective hold progress, controlling/holding faction, remaining checks/turns, and reset/interruption reason must be visible in the strategic HUD/status/result feedback.
6. If another faction controls or contests the objective before the next valid check, prior progress resets for MVP.
7. Champion defeat victory still has priority over objective hold victory after battle/result application.

## Source authority

Approved implementation sources:

- `design/gdd/strategic-map.md` §10 Site and Infrastructure States, especially site preview/control/guarded/contested state rules.
- `design/gdd/strategic-map.md` §13 Turn/Scenario/Victory Structure, especially:
  - start-of-faction-turn objective check;
  - central objective hold victory;
  - working default of 2 consecutive own-turn checks;
  - objective hold state fields;
  - objective control contract and reset visibility.
- `docs/architecture/control-manifest.md` §§1, 2, 4, 5, 6, 7, 9, 10.
- `docs/architecture/testing-strategy.md`.
- `docs/architecture/ci-build-automation.md`.

Prior objective stories are context and regression surface, not permission to keep immediate objective victory if that contradicts this READY story.

## In scope

- Runtime state/support for central-objective hold progress using stable fields equivalent to:
  - objective site ID;
  - holding/controlling faction ID;
  - hold progress;
  - required hold count.
- Strategic rules so central objective capture/control starts or advances a countdown instead of same-interaction victory.
- Start-of-own-turn objective progress/victory evaluation consistent with Strategic Map §13.
- Reset/interrupt behavior when the objective becomes controlled/contested by the other faction before the holder completes the countdown.
- Strategic HUD/status/result text that tells the player:
  - who controls or is holding the objective;
  - current progress and required progress;
  - how many own-turn checks remain;
  - that the opponent has a counterplay window;
  - why progress reset or did not advance.
- Focused EditMode/PlayMode tests and evidence proving the countdown, reset, and visible feedback.

## Out of scope

- No round-based defense waves.
- No multi-objective control-points system.
- No scoring/race victory mode.
- No new tactical battle modes, tactical objective redesign, or tactical AI behavior.
- No strategic AI.
- No fog/stealth/hidden objective state.
- No new map layout or final art/VFX/audio.
- No campaign persistence/save-load format expansion beyond serializable state fields needed by this story.
- No Champion recovery/revival/capture rules.
- No broader economy, Intel, Operations, Command, recruitment, or faction-specific objective rules.

## Allowed placeholders / assumptions

- Use clear prototype UI text instead of final narrative copy.
- Use existing strategic HUD/status/result presentation surfaces where practical; do not build a full objective panel unless needed for readability.
- The first scenario may use the existing central objective site and a default required hold count of 2 from data/configuration.
- If the current runtime lacks fully separate `contested` state, implement the smallest equivalent interruption/reset behavior and label the limitation in evidence; do not invent a full contest/control-points model.

## Acceptance criteria

- Capturing/interacting with the central objective no longer wins immediately from the same interaction alone.
- The objective records visible hold progress for the acting/controlling faction.
- At the next valid own-turn objective check, holding the objective advances progress and only wins when required progress is met.
- `objectiveHoldRequired` is data/state driven for the scenario, with working default 2.
- If the opposing faction takes/control-contests the objective before completion, prior holder progress resets and the UI/result feedback explains the reset or interruption.
- Champion defeat victory remains immediate priority after battle/result application and is not delayed by objective countdown logic.
- Strategic HUD/status/result feedback shows controlling/holding faction, progress, turns/checks remaining, and opponent counterplay window.
- Invalid or unavailable objective interactions explain why and do not partially mutate hidden objective progress.
- Existing objective, Champion encounter, guarded-site, command explanation, and loop smoke behavior is not regressed outside the approved objective timing change.

## Evidence requirements

Implementation PR must include `production/evidence/STORY-STRAT-OBJECTIVE-001/README.md` with:

- tests run;
- exact-head Unity Foundation CI URL;
- screenshots/PNG evidence or equivalent PlayMode evidence showing:
  1. initial objective capture/hold progress without immediate victory;
  2. start-of-own-turn progress/victory countdown state;
  3. opponent reset/interruption or counterplay feedback;
  4. final objective victory only after the required hold progress;
- omissions/deferred-work section, or `No known omissions`.

## Branch / PR

- Branch: `story/STORY-STRAT-OBJECTIVE-001-multi-turn-objective-contest-direction`
- PR title: `STORY-STRAT-OBJECTIVE-001 Multi-turn objective contest direction`
- One READY story per branch. Do not bundle unrelated cleanup unless required to make this story pass its tests/evidence.

## Ambiguity Check

Status: PASS.

Resolved decisions:

- Objective rule shape: Option 1, two-turn capture countdown.
- Victory timing: objective victory requires later own-turn hold progress; not same-interaction sneak capture.
- Interruption default: opposing control/contest before completion resets prior progress for MVP.
- Scope boundary: no defense waves, no control-points system, no broader objective redesign.

## Readiness gate

- [x] Story status is READY.
- [x] Human approval is recorded.
- [x] Source authority is approved or narrowly scoped.
- [x] Acceptance criteria are testable.
- [x] Non-goals and placeholders are explicit.
- [x] Evidence requirements are explicit.
- [x] Branch/PR guidance is explicit.

Verdict: DONE / merged. Objective countdown implementation passed merge gate, exact-head PR CI, and post-merge main CI.
