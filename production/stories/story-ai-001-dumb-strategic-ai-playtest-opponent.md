---
title: STORY-AI-001 Dumb Strategic AI Playtest Opponent
type: story
status: ready
phase: production
owner: shared
created: 2026-07-08
updated: 2026-07-08
source_lore: []
related:
  [
    production/epics/epic-vslice-mvp-015-post-audit-foundation-pivot-and-reconciliation,
    production/planning/post-audit-foundation-pivot-2026-07-03,
    docs/architecture/data-scenario-save-format-adr,
    docs/architecture/determinism-and-rng-adr,
    docs/architecture/control-manifest,
    docs/architecture/testing-strategy,
    docs/architecture/ci-build-automation,
    design/gdd/strategic-map,
  ]
approval: approved
---

# STORY-AI-001 Dumb Strategic AI Playtest Opponent

## Status

READY / approved. Promoted 2026-07-08 after `STORY-DETERMINISM-001` merged and post-merge publish CI passed. This is the next EPIC-015 implementation packet and authorizes a narrow Unity runtime slice only through the scope below.

Pointer evidence:

- Unity pointer PR: https://github.com/myriwe-bot/neon-champions-unity/pull/140
- Pointer merge commit: `d18b25bf21441005ac543ef7b542c0c1cf5236db`
- Exact-head pointer PR CI: https://github.com/myriwe-bot/neon-champions-unity/actions/runs/28923730106
- Post-merge pointer main CI: https://github.com/myriwe-bot/neon-champions-unity/actions/runs/28924095023

## Story type

Logic/AI + Playtest Support.

## Parent epic

- `production/epics/epic-vslice-mvp-015-post-audit-foundation-pivot-and-reconciliation.md`.

## User/player/system value

As a solo tester, I need a dumb deterministic strategic opponent, so playtests can validate pacing, pressure, objective ownership, and site interactions without requiring a second human to drive faction 2.

## Source requirements

- Pivot brief: `production/planning/post-audit-foundation-pivot-2026-07-03.md` approved a "dumb strategic AI plan/story for single-player-valid playtests" and excludes sophisticated strategic AI.
- Data/scenario/save ADR: scenario data, runtime state, and save shape stay separate; current scenario data path is the authority for implemented content values.
- Determinism/RNG ADR: AI behavior must be deterministic unless a later seeded RNG story is approved.
- Control manifest/testing/CI docs: implementation must be source-authorized, testable, and CI-gated.
- Strategic map GDD: current MVP is deterministic strategic movement, site interaction, turn ownership, objective pressure, and tactical handoff.

## In scope

- Add the smallest deterministic strategic AI controller/service needed for a `ControllerType.StrategicAI` faction to take one legal strategic turn in the current smoke scenario.
- Prefer a simple priority order such as: select active AI Champion, take the first deterministic legal route toward useful pressure/objective/site interaction, apply one available site interaction when legal and useful, then end the AI turn.
- Add or update scenario data so faction 2 can be marked `StrategicAI` for the AI smoke path without breaking current hotseat/human-local tests.
- Expose clear snapshot/HUD/status text that the active faction is AI-controlled and what action the dumb AI took.
- Add focused EditMode tests for deterministic choice order, invalid/no-legal-action handling, turn advancement, and no unseeded random use.
- Add PlayMode/smoke evidence showing a human-to-AI-to-human turn cycle in the current scenario.

## Out of scope

- Sophisticated strategic planning, minimax, utility scoring, learning, personality, diplomacy, fog/dirty-information reasoning, deception, or hidden-info rolls.
- Tactical CombatAI changes beyond preserving existing tactical handoff behavior.
- New factions, new map topology, new campaign content, new objective rules, or balance changes.
- Seeded or unseeded randomness.
- Full save/load or replay implementation.
- Editor UI or scenario-authoring tools.

## Allowed stubs, mocks, placeholders, or temporary data

- A single deterministic hardcoded priority list is allowed if scoped to current scenario/system IDs and documented as temporary MVP AI behavior.
- A test-only or scenario-data toggle for `ControllerType.StrategicAI` is allowed if it does not replace the human-local baseline.
- If no legal action exists, the AI may emit a clear diagnostic/status and end turn deterministically.

## Dependencies

- `STORY-DATA-001` DONE / merged.
- `STORY-DETERMINISM-001` DONE / merged; deterministic-by-default policy approved.
- Unity README current-task pointer names this story through PR #140; exact-head and post-merge pointer CI passed.

## Acceptance criteria

- [ ] A `ControllerType.StrategicAI` faction can execute a deterministic one-turn strategic action path in the current scenario.
- [ ] The AI never uses `UnityEngine.Random`, `System.Random`, time/GUID entropy, or unordered collection iteration as choice behavior.
- [ ] The AI action path is reproducible from the same scenario/runtime state and command order.
- [ ] Existing human-local hotseat path remains valid.
- [ ] Snapshot/HUD/status text makes AI control and AI action results visible enough for playtest notes.
- [ ] Tests cover deterministic priority order, no-legal-action/invalid-state handling, and turn handoff back to the human faction.
- [ ] Evidence records exact commands, CI URL placeholder/final URL, omissions, and what remains dumb/deferred.

## Verification requirements

- `git diff --check`.
- Focused EditMode tests for the strategic AI controller/service and scenario controller data.
- Relevant PlayMode/smoke test or evidence capture for human -> AI -> human turn cycle.
- Existing strategic input/turn/snapshot tests updated only where the approved AI controller path requires it.
- Exact-head Unity Foundation CI before merge; post-merge main CI after merge.
- PR omissions section listing strategic AI behaviors explicitly deferred.

## Ambiguity Check

Status: PASS for implementation.

Resolved assumptions:

- "Dumb strategic AI" means deterministic playtest pressure, not competent opponent design.
- Faction 2 is the default AI candidate for the current smoke scenario, but the story must preserve the existing human-local baseline or test path.
- The AI may be visibly crude if its action choice is deterministic, legal, tested, and documented.
- Any desired random or probabilistic AI behavior is blocked by the determinism ADR until a seeded RNG story exists.

## Branch / PR requirements

- Branch name: `story/STORY-AI-001-dumb-strategic-ai-playtest-opponent`.
- PR title: `STORY-AI-001 dumb strategic AI playtest opponent`.
- Required linked story ID: `STORY-AI-001`.
- Required evidence path: `production/evidence/STORY-AI-001/`.
- Codex must commit and push the implementation branch to remote, or clearly explain why it stopped without pushing.

## Story readiness gate

- [x] Story has stable ID, title, type, status, and parent epic.
- [x] User/system value is clear.
- [x] Exact ADR/architecture/control-manifest sources are linked.
- [x] In-scope work is concrete and bounded.
- [x] Out-of-scope work is explicit.
- [x] Verification requirements are defined.
- [x] Human-approved pivot source includes dumb strategic AI as an approved EPIC-015 output.
- [x] Determinism constraint is explicit.

## Runnable prompt

Runnable prompt: `production/sprints/codex-story-ai-001.prompt.txt`. It keeps preflight guards for `status: ready`, `approval: approved`, Ambiguity Check PASS, `STORY-DETERMINISM-001` DONE/merged, and Unity README pointer agreement.

## Verdict

READY / approved. Implement only the narrow deterministic playtest-opponent slice; defer sophisticated AI and all random behavior.
