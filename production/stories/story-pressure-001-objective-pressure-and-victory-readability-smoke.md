---
title: STORY-PRESSURE-001 Objective Pressure and Victory Readability Smoke
type: story
status: done
phase: production
owner: shared
created: 2026-07-01
updated: 2026-07-02
source_lore: []
related:
  [
    production/epics/epic-vslice-mvp-013-scenario-pressure-and-victory-readability,
    production/planning/next-implementation-direction-brief-2026-07-01,
    production/epics/epic-vslice-mvp-003-scenario-objective-champion-combat-and-casualty-stakes,
    production/epics/epic-vslice-mvp-012-intel-leads-and-verification,
    design/gdd/strategic-map,
    design/gdd/tactical-combat,
    docs/architecture/control-manifest,
    docs/architecture/testing-strategy,
    docs/architecture/ci-build-automation,
  ]
approval: approved
---

# STORY-PRESSURE-001 Objective Pressure and Victory Readability Smoke

## Status

DONE / merged. Unity PR #127 merged as `a0292f1bb2683e28a4284d29e6b090d8bb7552ed`; exact-head PR CI passed at https://github.com/myriwe-bot/neon-champions-unity/actions/runs/28539704598 and post-merge `main` CI passed at https://github.com/myriwe-bot/neon-champions-unity/actions/runs/28567436916.

Unity current-task pointer PR #126 merged as `3b69cc1a22658d2b7caf9b7a32e10739bcc2ad52`; exact-head pointer PR CI passed at https://github.com/myriwe-bot/neon-champions-unity/actions/runs/28534876195 and post-merge pointer main CI passed at https://github.com/myriwe-bot/neon-champions-unity/actions/runs/28535330443.

## Story type

Strategic UX + connected PlayMode smoke / readability pass.

## Parent / context

Parent: `EPIC-VSLICE-MVP-013 Scenario Pressure and Victory Readability`.

The prototype already has objective/victory hooks, tactical handoff/result slices, map readability, recruitment/base/economy slices, terrain/context slices, and a closed Intel Lead/Verification layer. The next safe step is to clarify the current scenario pressure and win/loss direction in one connected proof path, not to add a new campaign, full AI, economy, or tactical mechanic.

## Player/design value

As a tester, I need to see what is pressuring me, what action can change the objective/victory state, and how the game communicates success/failure direction, so I can judge whether the current prototype loop is playable rather than only technically connected.

## Source authority

Required sources:

- `production/planning/next-implementation-direction-brief-2026-07-01.md`.
- `production/epics/epic-vslice-mvp-013-scenario-pressure-and-victory-readability.md`.
- `production/epics/epic-vslice-mvp-003-scenario-objective-champion-combat-and-casualty-stakes.md` and merged objective/victory evidence.
- `production/stories/story-obj-001-scenario-objective-state-and-victory-feedback.md`.
- `production/stories/story-loop-004-objective-champion-combat-and-casualty-stakes-smoke.md`.
- `production/epics/epic-vslice-mvp-012-intel-leads-and-verification.md` for current closed Intel-layer context only.
- `design/gdd/strategic-map.md` §§6, 8, 10-14.
- `design/gdd/tactical-combat.md` existing tactical handoff/result boundaries.
- `docs/architecture/control-manifest.md`, `docs/architecture/testing-strategy.md`, `docs/architecture/ci-build-automation.md`.

## In scope

- Add or refine one connected PlayMode/evidence path across existing objective/victory/strategic-loop surfaces:
  1. show current objective pressure before the player changes it;
  2. show what action/path can reduce, contest, or resolve that pressure using existing mechanics;
  3. show the pressure/victory direction after that action;
  4. show clear success/failure/victory/loss-direction feedback where current systems support it;
  5. prove surrounding strategic interaction remains usable after the pressure/victory messaging exists.
- Minimal HUD/status/evidence-label copy or presentation adjustments needed to make the current objective pressure readable.
- Focused tests only where needed to cover state-backed pressure/victory/readability behavior and regressions.
- PlayMode/generated PNG or text evidence under Unity `production/evidence/STORY-PRESSURE-001/`.
- A concise implementation evidence note naming any remaining pressure/victory/playability gaps that should be human-reviewed next.

## Out of scope

- New campaign mode, scenario generator, save/load, meta-progression, or multiple objective archetype framework.
- Broad strategic AI, enemy planning, autonomous turns, diplomacy, public PR, legitimacy, blackmail, social graph, or economy systems.
- New tactical combat mechanics, unit abilities, morale/cohesion, AP rules, terrain rules, balance, or battle-result semantics.
- New Intel Lead types, false/contested information, fog-of-war, counter-intel, or dirty-information operations.
- New map topology, routes, sites, objectives, resources, recruitment rules, base/facility systems, final content/lore names, art/audio/VFX/icons/localization/accessibility framework.

## Acceptance criteria

- [ ] Connected evidence shows objective/pressure status before the player changes it.
- [ ] Connected evidence shows a clear player action/path that changes or resolves current pressure using existing mechanics.
- [ ] Connected evidence shows after-state pressure/victory direction in player-facing text.
- [ ] The pressure/victory messaging is backed by runtime/application state or existing result objects, not screenshot-only copy.
- [ ] At least one normal strategic interaction remains visibly usable after the pressure/victory messaging exists.
- [ ] Existing objective/victory, tactical handoff/result, Intel readability, and surrounding-loop tests/evidence expectations continue to pass or are updated with equivalent stronger coverage.
- [ ] Evidence under Unity `production/evidence/STORY-PRESSURE-001/` includes before-pressure, pressure-action, after-pressure/victory-direction, surrounding-loop-unbroken, and omissions/deferred-work notes.
- [ ] Exact-head Unity Foundation CI passes before merge.

## Verification requirements

Required unless a blocker is documented in PR evidence:

- `git diff --check`.
- Focused EditMode/domain/application tests for any changed objective pressure, victory feedback, status copy, or result-state behavior.
- PlayMode smoke or generated PNG/text evidence for before-pressure, pressure-action, after-pressure/victory-direction, and surrounding-loop-unbroken states.
- Placeholder validator.
- Standalone Windows64 build if the Unity CI workflow runs it.
- Exact-head Unity Foundation CI before merge and post-merge main CI after merge.

## Ambiguity Check

Status: PASS. Implementation authority granted for one objective-pressure/victory-readability smoke only.

Human-approved answers / assumptions:

- The approved next direction is Scenario pressure and victory readability.
- First slice is `STORY-PRESSURE-001 Objective Pressure and Victory Readability Smoke`.
- Use existing objective/victory and strategic-loop mechanics; do not invent new campaign, AI, economy, tactical, or dirty-information systems.
- If implementation already satisfies part of the story, Codex should focus on tests/evidence/readability gaps rather than inventing new mechanics.

## Branch / PR requirements

- Branch name: `story/STORY-PRESSURE-001-objective-pressure-victory-readability`.
- PR title: `STORY-PRESSURE-001 objective pressure and victory readability smoke`.
- Required linked story ID: `STORY-PRESSURE-001`.
- Required evidence path: `production/evidence/STORY-PRESSURE-001/` in Unity.
- Required omissions section: explicitly list deferred campaign/AI/economy/tactical/dirty-information systems or state `No known omissions`.

## Story readiness gate

- [x] Story has stable ID, title, type, status, and parent/context.
- [x] User/player/system value is clear.
- [x] Source authority is explicit.
- [x] In-scope and out-of-scope are bounded.
- [x] Acceptance criteria are observable.
- [x] Verification requirements are defined.
- [x] Branch / PR / CI traceability requirements are stated.
- [x] Ambiguity Check is PASS.
- [x] Human implementation approval has been recorded.

## Verdict

DONE. The narrow objective-pressure/victory-readability smoke merged in Unity PR #127 and post-merge `main` CI passed. Broader campaign, AI, economy, tactical, and dirty-information systems remain deferred.
