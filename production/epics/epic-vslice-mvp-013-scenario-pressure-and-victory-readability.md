---
title: EPIC-VSLICE-MVP-013 Scenario Pressure and Victory Readability
type: epic
status: approved
phase: production
owner: shared
created: 2026-07-01
updated: 2026-07-01
source_lore: []
related:
  [
    design/gdd/game-pillars,
    design/gdd/strategic-map,
    design/gdd/tactical-combat,
    docs/architecture/control-manifest,
    docs/architecture/testing-strategy,
    docs/architecture/ci-build-automation,
    production/planning/next-implementation-direction-brief-2026-07-01,
    production/epics/epic-vslice-mvp-012-intel-leads-and-verification,
    production/stories/story-pressure-001-objective-pressure-and-victory-readability-smoke,
  ]
approval: approved
---

# Epic: EPIC-VSLICE-MVP-013 Scenario Pressure and Victory Readability

## Status

APPROVED / IN PROGRESS. Human approval recorded 2026-07-01: "approved" for the recommended next direction in `production/planning/next-implementation-direction-brief-2026-07-01.md`. `STORY-PRESSURE-001 Objective Pressure and Victory Readability Smoke` is READY / approved as the current Unity implementation packet.

## Capability goal

Convert the accumulated strategic, tactical, objective, and Intel slices into a clearer playable pressure loop. A tester should understand what objective pressure exists, what action changes it, and how victory/loss direction is communicated without adding a full campaign, broad AI, or new economy.

## Player / design value

As a player/tester, I need the prototype to tell me what is pressuring me and how my actions move the scenario toward victory or loss, so I can judge the game loop rather than only disconnected mechanics.

## Source requirements

- `production/planning/next-implementation-direction-brief-2026-07-01.md` for approved direction/defaults.
- `production/epics/epic-vslice-mvp-003-scenario-objective-champion-combat-and-casualty-stakes.md` and merged objective/victory story evidence.
- `production/epics/epic-vslice-mvp-012-intel-leads-and-verification.md` and merged Intel-layer evidence as supporting status/context, not as new dirty-information scope.
- `design/gdd/strategic-map.md` §§6, 8, 10-14 for strategic map, objectives, sites, routes, resources/recruitment context, and victory hooks.
- `design/gdd/tactical-combat.md` for existing tactical handoff/result boundaries.
- `docs/architecture/control-manifest.md`, `docs/architecture/testing-strategy.md`, and `docs/architecture/ci-build-automation.md`.

## Scope

### In scope

- One narrow pressure/readability pass over existing scenario objective and victory/loss surfaces.
- Clear HUD/status text for current objective pressure, what is changing, and win/loss direction.
- One connected smoke proving a player can understand the pressure, perform an action that changes it, and see victory/loss feedback using existing prototype systems.
- Focused EditMode/PlayMode tests and generated evidence for the first implementation story.

### Out of scope

- New campaign mode, save/load, meta-progression, or scenario generator.
- Broad strategic AI, autonomous enemy planning, diplomacy, PR, legitimacy, or economy systems.
- New tactical combat mechanics, unit abilities, terrain rules, or battle balance.
- New Intel/dirty-information mechanics beyond using existing readable context where already present.
- New map topology, final art/audio/VFX/icons/localization/accessibility framework, or final content names.

## Child stories

Agents and Codex may not implement this epic directly. They may only implement READY child stories.

| Story                                                                                                                                                    | Status           | Type                                       | Depends On                                       | Evidence                  |
| -------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------- | ------------------------------------------ | ------------------------------------------------ | ------------------------- |
| [STORY-PRESSURE-001 Objective Pressure and Victory Readability Smoke](../stories/story-pressure-001-objective-pressure-and-victory-readability-smoke.md) | READY / approved | Strategic UX + connected smoke/readability | EPIC-012 DONE; objective/victory baseline exists | Pending Unity PR/evidence |

Allowed story statuses: Draft, NEEDS WORK, READY-candidate, READY, IN PROGRESS, REVIEW, DONE, BLOCKED.

## Risks

| Risk                                                  | Type    | Impact                    | Mitigation                                                                              |
| ----------------------------------------------------- | ------- | ------------------------- | --------------------------------------------------------------------------------------- |
| Pressure pass becomes full campaign/victory system    | Scope   | Large unbounded system    | First story is one connected readability smoke over existing objective/victory surfaces |
| Runtime adds fake pressure state only for screenshots | Quality | Misleading evidence       | Require state-backed assertions and connected PlayMode evidence                         |
| It hides remaining playability problems behind text   | UX      | Prototype still confusing | Evidence must include before/after pressure and surrounding-loop screenshots/notes      |

## Epic readiness gate

- [x] Capability goal is clear.
- [x] Human approved direction/default.
- [x] Relevant source authority is explicit.
- [x] Scope and out-of-scope are bounded.
- [x] First child story is identified and READY / approved.
- [x] Required test/evidence layers are known.
- [x] No Unity implementation is authorized by the epic alone.

## Verdict

APPROVED / IN PROGRESS. Implement only READY child stories. `STORY-PRESSURE-001` is the current approved implementation packet; broader campaign, AI, economy, tactical, and dirty-information systems remain deferred.
