---
title: STORY-STRAT-002 Hotseat Turn Ownership
type: story
status: approved
phase: production
owner: shared
created: 2026-06-02
updated: 2026-06-02
source_lore: []
related:
  [
    design/gdd/strategic-map,
    docs/architecture/unity-technical-scheme,
    docs/architecture/control-manifest,
    docs/architecture/testing-strategy,
    docs/architecture/ci-build-automation,
    production/epics/epic-strat-mvp-001-strategic-mvp-core-loop,
    production/stories/story-strat-001-scenario-map-graph-state,
  ]
approval: approved
---

# Story: STORY-STRAT-002 Hotseat Turn Ownership

## Status

READY. Human approval recorded; this story may be assigned to Codex under the story train execution contract.

## Story type

Logic.

Primary layer: pure strategic-domain turn state and deterministic turn advancement.

## Estimate

- Size: S.
- Basis: readiness review on 2026-06-02; estimate covers story-scoped implementation and required evidence only.

## Parent epic

- Epic ID/path: [[production/epics/epic-strat-mvp-001-strategic-mvp-core-loop|EPIC-STRAT-MVP-001 Strategic MVP Core Loop]].

## User/player/system value

As a system, I want deterministic two-faction local-hotseat turn ownership, so that later movement, site interaction, income, objective checks, and victory evaluation happen for the correct active faction without requiring strategic AI or UI.

## Source requirements

Exact source references:

- GDD path + section/rule:
  - `design/gdd/strategic-map.md` §2 Approved MVP Direction, rules 2-5 and 7-8.
  - `design/gdd/strategic-map.md` §6 Core Loop Contract, steps 2, 10, and 11.
  - `design/gdd/strategic-map.md` §12 Champion/Army Strategic State and Movement Allowance, movement and interaction contract rule 1.
  - `design/gdd/strategic-map.md` §13 Turn/Scenario/Victory Structure, rules 1-8, start-of-faction-turn sequence, end-of-faction-turn sequence, and scenario state minimum.
- ADR / architecture section / control-manifest rule:
  - `docs/architecture/unity-technical-scheme.md` — domain logic separate from Unity presentation.
  - `docs/architecture/control-manifest.md` §§1, 2, 4, 5, 6, 9, 10.
  - `docs/architecture/testing-strategy.md` — story-type evidence matrix and TDD requirement.
  - `docs/architecture/ci-build-automation.md` — CI evidence requirements.
- UX/content/art/worldbuilding:
  - N/A. This story is domain logic only.

## In scope

- Add a pure domain turn service/controller for `ScenarioRuntimeState`.
- Begin/start active faction turn behavior:
  - active faction is read from `ActiveFactionId` and `TurnOrder`;
  - active faction Champion movement points reset to maximum;
  - active faction Champion major interaction availability resets to true;
  - objective hold progress may be checked only using existing central-objective fields; no new UI.
- End active faction turn behavior:
  - validate the active faction exists in turn order;
  - advance to the next faction in `TurnOrder`;
  - increment `TurnNumber` each faction turn;
  - increment `RoundNumber` when turn order wraps back to the first faction.
- Add clear validation/diagnostics for invalid turn state.
- Add EditMode/domain tests for turn initialization, reset, advancement, and invalid state.

## Out of scope

- UI, HUD, input, camera, scene, prefab, or player prompts.
- Strategic AI, online/networked multiplayer, simultaneous turns, or auto-end planning.
- Champion movement execution beyond resetting existing movement/action fields.
- Site interaction, rewards, recruitment, battle handoff, or result application.
- Recurring income implementation except for a no-op hook if needed and explicitly tested as no-op.
- New save/load system or final persistence format.
- New lore/content/faction/site names.

## Allowed stubs, mocks, placeholders, or temporary data

Allowed:

- Test-local scenario fixture from STORY-STRAT-001 or equivalent test-local data.
- No-op extension point for future recurring income only if clearly named/tested as not implemented.

Not allowed:

- Hidden automatic site rewards, movement, AI decisions, or UI behavior.

## Dependencies

- Required prior stories:
  - STORY-STRAT-001 implemented and merged or available on the implementation branch.
- Required architecture decisions:
  - Approved Unity technical scheme, control manifest, testing strategy, and CI/build automation.
- Required Unity/package setup:
  - Existing Unity domain/test assemblies and CI from SPIKE-001.

## Acceptance criteria

- [ ] Given an initialized two-faction scenario runtime, when the turn service begins the active faction turn, then that faction's Champion movement points equal maximum and major interaction availability is true.
- [ ] Given Faction 1 is active in a two-faction turn order, when end turn is applied, then Faction 2 becomes active and `TurnNumber` increments by one.
- [ ] Given Faction 2 is active and turn order wraps to Faction 1, when end turn is applied, then Faction 1 becomes active, `TurnNumber` increments by one, and `RoundNumber` increments by one.
- [ ] Given preview/validation of end turn if implemented, then preview does not mutate runtime state.
- [ ] Given an active faction ID not present in turn order, when end turn validation runs, then validation fails with a clear diagnostic.
- [ ] Given a missing/empty turn order, when turn validation runs, then validation fails with a clear diagnostic.
- [ ] Given a scenario with victory already resolved, when end turn is requested, then behavior is rejected or no-op according to a documented diagnostic; it must not silently advance play.
- [ ] Domain turn code compiles without UnityEngine, MonoBehaviour, ScriptableObject, scene, prefab, input, camera, or UI references.

## Verification requirements

- Unit tests: N/A unless a non-Unity pure C# runner exists.
- Unity edit-mode tests: Required for turn validation, start-turn reset, end-turn advancement, wrap/round increment, and invalid state diagnostics.
- Unity play-mode tests: N/A; no scene/prefab/UI behavior is authorized.
- Integration/data validation tests: N/A beyond domain/EditMode tests.
- Manual Unity scene/prefab checks: N/A.
- Screenshot/video evidence: N/A.
- Performance budget or N/A: N/A for small deterministic domain operations.
- CI evidence: Required on implementation PR.
- Playtest evidence: N/A.
- TDD evidence required? Yes.
- Automation deferred? No.

## Ambiguity Check

Status: PASS.

Open questions:

- None for domain turn ownership.

Assumptions:

- STORY-STRAT-001 runtime fields remain the state source: `ActiveFactionId`, `TurnOrder`, `TurnNumber`, `RoundNumber`, Champion movement and interaction fields, and `Victory`.

Out of scope:

- Same as story Out of scope section.

Allowed stubs/mocks:

- Same as Allowed stubs section.

Human approval:

- Approved by human on 2026-06-02 in response to readiness review.

Human-approved exceptions:

- None.

## Branch / PR requirements

- Branch name: `story/STORY-STRAT-002-hotseat-turn-ownership`
- PR title: `STORY-STRAT-002 Hotseat turn ownership`
- Required linked story ID: `STORY-STRAT-002`
- Required linked GDD/ADR/control docs:
  - `design/gdd/strategic-map.md` §§2, 6, 12, 13.
  - `docs/architecture/control-manifest.md` §§1, 2, 4, 5, 6, 9, 10.
  - `docs/architecture/testing-strategy.md` and `docs/architecture/ci-build-automation.md`.
- Required root/scoped AGENTS.md instructions: Unity repo root `AGENTS.md` and scoped source/test `AGENTS.md` under touched paths.
- Required evidence summary: RED/GREEN TDD summary, tests added/changed, CI link/status, omissions section.

PR must explicitly list known omissions, stubs, mocks, assumptions, deferred work, or state `No known omissions`.

## Story readiness gate

- [x] Story has stable ID, title, type, status, and parent epic.
- [x] User/player/system value is clear.
- [x] Exact GDD source section is linked or explicitly N/A.
- [x] Exact ADR/architecture/control-manifest source is linked or explicitly N/A.
- [x] Relevant root/scoped AGENTS.md instructions are identified.
- [x] UX/content/art/worldbuilding references are N/A.
- [x] In-scope work is concrete and bounded.
- [x] Out-of-scope work is explicit.
- [x] Stubs/mocks/placeholders are either disallowed or explicitly listed.
- [x] Dependencies are listed.
- [x] Acceptance criteria are observable and testable.
- [x] Verification requirements are defined.
- [x] Required automated tests/validators/PlayMode evidence are listed or N/A.
- [x] Ambiguity Check status is PASS.
- [x] Branch / PR / CI traceability requirements are stated.
- [x] Estimate is recorded.
- [x] Human approval has been given or delegated gate approval is recorded.
  - Approved by human on 2026-06-02 in response to readiness review.

## DONE gate

- [ ] Implementation matches approved story scope.
- [ ] Acceptance criteria pass.
- [ ] Required verification evidence exists.
- [ ] Required automated tests and CI pass or approved exceptions are documented.
- [ ] No unauthorized design or architecture decisions were introduced.
- [ ] Omissions/stubs/mocks/deferred work are documented.
- [ ] PR/code review is complete.
- [ ] Required docs were updated in the correct source-of-truth layer.

## Verdict

READY. Gate blockers: none.
