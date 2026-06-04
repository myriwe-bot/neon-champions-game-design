---
title: STORY-STRAT-004 Site Interaction and Guarded Battle Trigger
type: story
status: done
phase: production
owner: shared
created: 2026-06-04
updated: 2026-06-04
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
    production/stories/story-strat-002-hotseat-turn-ownership,
    production/stories/story-strat-003-champion-route-movement,
    production/stories/story-tac-001-battle-setup-result-dto-contracts,
  ]
approval: approved
---

# Story: STORY-STRAT-004 Site Interaction and Guarded Battle Trigger

## Status

DONE / merged in Unity PR #13. Merge commit: `9e0276a24069c2bd7056ced5029d01d714a37f1c`. Post-merge Unity main CI passed on 2026-06-04.

## Story type

Logic + Integration.

## Estimate

- Size: M.
- Basis: adds site interaction command/preview/apply plus guarded-site `BattleSetup` creation, but deliberately does not resolve battles or apply rewards/results.

## Parent epic

- Epic ID/path: `production/epics/epic-strat-mvp-001-strategic-mvp-core-loop.md`.

## User/player/system value

As a player, I want selecting a guarded site to clearly preview and launch a battle handoff, so that the strategic map begins to connect movement decisions to tactical encounters without tactical combat mutating strategic state.

## Source requirements

Exact source references:

- GDD path + section/rule:
  - `design/gdd/strategic-map.md` §6 Core Loop Contract, steps 5-7.
  - `design/gdd/strategic-map.md` §10 Site and Infrastructure States, rules 1-8, runtime states, ownership/control contract rules 1-6.
  - `design/gdd/strategic-map.md` §12 Champion/Army Strategic State and Movement Allowance, rules 9-12 and movement/interaction contract rules 3-5.
  - `design/gdd/strategic-map.md` §14 Strategy-to-Tactical DTOs, BattleSetup minimum and minimum strategic loop test cases 1 and 7.
- ADR / architecture section / control-manifest rule:
  - `docs/architecture/unity-technical-scheme.md` — domain logic separated from Unity presentation.
  - `docs/architecture/control-manifest.md` §§1, 2, 4, 5, 6, 7, 9, 10.
  - `docs/architecture/testing-strategy.md` — TDD and story evidence requirements.
  - `docs/architecture/ci-build-automation.md` — CI evidence requirements.
- UX/content/art/worldbuilding:
  - No new final lore, faction naming, site naming, art, icons, audio, animation, or copy. Placeholder/localization keys only.
- Parent epic:
  - `production/epics/epic-strat-mvp-001-strategic-mvp-core-loop.md`.

## In scope

Concrete implementation tasks authorized by this story:

- Add or extend pure domain models for site definitions/runtime state sufficient to represent a guarded neutral site attached to a strategic node.
- Add `SiteInteractionCommand` or equivalent with preview/apply mode.
- Add validation that the active Champion/faction can interact with the target site only when:
  - the Champion is at the site's node;
  - it is the Champion owner's active faction turn;
  - the Champion has a major interaction available;
  - the site is interactable and guarded;
  - required IDs and guard army data are present.
- Add preview behavior that reports expected interaction type, source site/node, battle type, attacker/defender roles, and guard/reward context without mutating strategic runtime state.
- Add apply behavior that creates a valid `BattleSetup` for a guarded neutral site using the DTO contract from STORY-TAC-001.
- Mark or expose an unresolved/pending battle reference only as needed to prevent duplicate launch from the same command.
- Consume the Champion's major interaction when the battle is launched.
- Add a visible Unity path using the existing strategic map scene/HUD/input patterns: the player selects a guarded site marker, the HUD shows a guarded-site Attack/Interact affordance/summary, and the player launches the guarded-site battle handoff.
- Add tests proving preview is non-mutating and apply creates a valid guarded-site `BattleSetup`.

## Out of scope

Adjacent behavior not authorized by this story:

- Tactical combat execution, tactical scene loading, tactical map/grid, combat AI, AP/actions, damage, morale, animation, or tactical UI.
- Applying `BattleResult` to strategic state; that belongs to STORY-STRAT-005.
- Clearing guards, claiming site control, granting rewards, resource stockpile changes, recruitment, recurring income, objective hold progress, or victory evaluation.
- Enemy faction site contests, Champion-vs-Champion battles, garrisons, retreats, capture, wounded/recovery, save/load, strategic AI, networking, final art/UI/copy.
- New player-facing Greenland scenario content or final site names.

## Allowed stubs, mocks, placeholders, or temporary data

Allowed:

- Test-local guarded site definitions and guard army templates.
- Placeholder stable IDs and localization keys.
- Existing DTO placeholder battle types/controllers/outcome flags from STORY-TAC-001.
- A minimal unresolved battle marker if needed for validation.

Not allowed:

- Fake tactical resolution that pretends a battle completed.
- Direct resource/control mutation during preview or BattleSetup creation.
- Final site theme/content decisions.

## Dependencies

- Required prior stories:
  - STORY-STRAT-001 scenario/map graph state.
  - STORY-STRAT-002 hotseat turn ownership.
  - STORY-STRAT-003 Champion route movement.
  - STORY-TAC-001 battle setup/result DTO contracts.
- Required data/assets:
  - Existing test-local scenario/map/champion/army fixtures are enough.
- Required architecture decisions:
  - Approved Unity technical scheme, control manifest, testing strategy, and CI/build automation.
- Required Unity/package setup:
  - Existing Unity project and CI from SPIKE-001.

## Acceptance criteria

- [ ] Given an active Champion standing on a node with a guarded neutral site, when site interaction is previewed, then the result describes a guarded-site battle handoff and does not mutate Champion, site, resource, army, turn, or battle state.
- [ ] Given the same valid state, when site interaction is applied, then a valid `BattleSetup` is created with battle ID, scenario/source/site/node IDs, `GuardedSite` battle type, HumanLocal attacker controller, CombatAI/guard defender controller, attacking Champion army snapshot, and defending guard army snapshot.
- [ ] Given a guarded-site battle is launched, then the Champion's major interaction is consumed and duplicate launch is rejected or reported until the unresolved battle is handled.
- [ ] Given the Champion is not at the site node, it is not the Champion owner's turn, the Champion has no major interaction, the site is not guarded/interactable, or guard army data is missing, when interaction is previewed or applied, then validation fails with clear diagnostics and no state mutation.
- [ ] Given source strategic army/site state changes after `BattleSetup` creation in a test, then the `BattleSetup` army snapshots remain unchanged.
- [ ] Domain logic compiles without UnityEngine, scene, prefab, camera, input, or final UI dependencies.

## Verification requirements

- Unit tests: N/A unless a non-Unity pure C# runner exists.
- Unity edit-mode tests: Required for validation, preview non-mutation, apply `BattleSetup` creation, major-interaction consumption, duplicate prevention, and invalid diagnostics.
- Unity play-mode tests: Required for the visible strategic-map path if existing scene/test harness can support it; otherwise document the exact blocker and provide manual screenshot/video evidence as a temporary exception.
- Integration/data validation tests: Required if implementation adds serialized site fixtures or validators.
- Manual Unity scene/prefab checks: Required if scene/HUD/input is touched.
- Screenshot/video evidence: Required for visible interaction/handoff evidence.
- Performance budget or N/A: N/A for small domain command validation.
- CI evidence: Required on implementation PR.
- Playtest evidence: N/A.
- TDD evidence required? Yes.
- Automation deferred? No.

If a verification type is N/A, the PR must say why.

## Ambiguity Check

Status: PASS.

Resolved by user on 2026-06-04:

- Include a visible path. This is not domain-only.
- Use interaction style A: select guarded site marker, then HUD shows Attack/Interact button for that specific site.

Approved defaults:

- Strategic state should hold an explicit pending battle record after launch so duplicate launch/result-application can be validated.
- Launching a guarded-site battle spends the Champion's major interaction even if a later tactical layer cancels or returns a cancel result.
- First guarded-site defender should use a stable neutral guard-side ID plus `CombatAI` tactical controller data; no actual combat AI behavior is implemented here.

Approved implementation assumptions:

- Default visible path: select guarded site marker, then use the smallest existing strategic HUD/input pattern to show an Attack/Interact button; do not introduce final UI framework, art, or tactical scene transition.

Out of scope:

- Same as story Out of scope section.

Allowed stubs/mocks:

- Same as Allowed stubs section.

Human-approved exceptions:

- None.

If status is FAIL, this story is not READY.

## Branch / PR requirements

- Branch name: `story/STORY-STRAT-004-site-interaction-guarded-battle-trigger`
- PR title: `STORY-STRAT-004 Site interaction and guarded battle trigger`
- Required linked story ID: `STORY-STRAT-004`
- Required linked GDD/ADR/control docs:
  - `design/gdd/strategic-map.md` §§6, 10, 12, 14.
  - `docs/architecture/control-manifest.md` §§1, 2, 4, 5, 6, 7, 9, 10.
  - `docs/architecture/testing-strategy.md` and `docs/architecture/ci-build-automation.md`.
- Required root/scoped AGENTS.md instructions: Unity repo root `AGENTS.md` and scoped source/test `AGENTS.md` under touched paths.
- Required evidence summary: RED/GREEN TDD summary, interaction tests, DTO validation evidence, CI link/status, omissions section.

PR must explicitly list known omissions, stubs, mocks, assumptions, deferred work, or state `No known omissions`.

## Story readiness gate

- [x] Story has stable ID, title, type, status, and parent epic.
- [x] User/player/system value is clear.
- [x] Exact GDD source section is linked or explicitly N/A.
- [x] Exact ADR/architecture/control-manifest source is linked or explicitly N/A.
- [x] Relevant root/scoped AGENTS.md instructions are identified.
- [x] UX/content/art/worldbuilding references are linked if relevant.
- [x] In-scope work is concrete and bounded.
- [x] Out-of-scope work is explicit.
- [x] Stubs/mocks/placeholders are either disallowed or explicitly listed.
- [x] Dependencies are listed.
- [x] Acceptance criteria are observable and testable.
- [x] Verification requirements are defined according to `docs/architecture/testing-strategy.md`.
- [x] Required automated tests/validators/PlayMode evidence are listed, or approved exceptions are documented.
- [x] Ambiguity Check status is PASS.
- [x] Branch / PR / CI traceability requirements are stated.
- [x] Human approval has been given or delegated gate approval is recorded: user approved the train and started with STORY-STRAT-004 on 2026-06-04.

## DONE gate

- [x] Implementation matches approved story scope.
- [x] Acceptance criteria pass.
- [x] Required verification evidence exists.
- [x] Required automated tests, validators, and PlayMode/smoke evidence pass, or human-approved exceptions are documented.
- [x] No unauthorized design or architecture decisions were introduced.
- [x] Omissions/stubs/mocks/deferred work are explicitly documented.
- [x] PR/code review is complete.
- [x] CI passes or human-approved exceptions are documented.
- [x] Required docs were updated in the correct source-of-truth layer.

## Verdict

DONE. Unity PR #13 merged on 2026-06-04 with post-merge main CI green.
