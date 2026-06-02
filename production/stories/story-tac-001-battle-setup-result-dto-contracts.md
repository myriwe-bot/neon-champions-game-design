---
title: STORY-TAC-001 Battle Setup Result DTO Contracts
type: story
status: in-review
phase: production
owner: shared
created: 2026-06-02
updated: 2026-06-02
source_lore: []
related: [design/gdd/strategic-map, design/gdd/tactical-combat, docs/architecture/unity-technical-scheme, docs/architecture/control-manifest, docs/architecture/testing-strategy, docs/architecture/ci-build-automation, production/epics/epic-strat-mvp-001-strategic-mvp-core-loop, production/stories/story-strat-001-scenario-map-graph-state]
approval: pending
---

# Story: STORY-TAC-001 Battle Setup Result DTO Contracts

## Status

READY-candidate. Requires explicit human approval before Codex implementation.

## Story type

Logic + Integration contract.

Primary layer: pure DTO boundary between strategic state and future tactical combat.

## Estimate

- Size: M.
- Basis: readiness review on 2026-06-02; estimate covers story-scoped implementation and required evidence only.

## Parent epic

- Epic ID/path: [[production/epics/epic-strat-mvp-001-strategic-mvp-core-loop|EPIC-STRAT-MVP-001 Strategic MVP Core Loop]].

## User/player/system value

As a system, I want explicit strategy-to-tactics battle setup and result DTOs, so that strategic stories can request and consume battles without tactical combat directly reading or mutating strategic runtime state.

## Source requirements

Exact source references:

- GDD path + section/rule:
  - `design/gdd/strategic-map.md` §6 Core Loop Contract, steps 6-8.
  - `design/gdd/strategic-map.md` §7 Data and State Contract Draft, BattleSetup and BattleResult rows.
  - `design/gdd/strategic-map.md` §10 Site and Infrastructure States, ownership/control contract rule 6.
  - `design/gdd/strategic-map.md` §12 Champion/Army Strategic State and Movement Allowance, movement and interaction contract rule 12 and army strategic state rules 2-5.
  - `design/gdd/strategic-map.md` §14 Strategy-to-Tactical DTOs, boundary rule, BattleSetup minimum, BattleResult minimum, strategic application contract, and minimum strategic loop test cases.
  - Binding implementation authority is `design/gdd/strategic-map.md` §14 plus the strategic-map sections above. `design/gdd/tactical-combat.md` and split tactical implementation contracts may be read only for compatibility; because they remain draft/pending, they must not add scope or block the DTO minimum unless they directly contradict strategic-map §14.
- ADR / architecture section / control-manifest rule:
  - `docs/architecture/unity-technical-scheme.md` — domain logic separate from Unity presentation and explicit module boundaries.
  - `docs/architecture/control-manifest.md` §§1, 2, 4, 5, 6, 7, 9, 10.
  - `docs/architecture/testing-strategy.md` — story-type evidence matrix and TDD requirement.
  - `docs/architecture/ci-build-automation.md` — CI evidence requirements.
- UX/content/art/worldbuilding:
  - N/A. DTO summary fields may use placeholder keys only; no player-facing copy/content decisions.

## In scope

- Add pure serializable-friendly DTOs/enums for:
  - `BattleSetup` or equivalent;
  - `BattleResult` or equivalent;
  - battle type/outcome/side/controller/result flags;
  - side snapshots containing faction, Champion optional reference, controller, and copied army state;
  - battle/result validation diagnostics.
- DTOs must use snapshots/copies of army state and IDs, not direct mutable references into strategic runtime state.
- Add validation for required IDs, sides, controllers, battle type, army snapshots, and setup/result battle ID matching helper if appropriate.
- Add tests proving DTOs are domain-only, serializable-friendly, and do not mutate strategic runtime state by construction.

## Out of scope

- Tactical combat engine, tactical map/grid, AP/actions, damage, AI, objectives, morale, UI, animation, scene, prefab, or camera.
- Strategic site interaction behavior that creates BattleSetup from a site; that belongs to STORY-STRAT-004 or later.
- Applying BattleResult to strategic state; that belongs to a later strategy result-application story.
- Player-facing battle summary text beyond placeholder keys/structured facts.
- New tactical unit roster/content/balance decisions.

## Allowed stubs, mocks, placeholders, or temporary data

Allowed:
- Placeholder enum values explicitly listed in strategic-map §14 such as `GuardedSite`, `SiteContest`, `ChampionVsChampion`, `AttackerWin`, `DefenderWin`, `Retreat`, `Cancelled`, `Draw`.
- Test-local army snapshots and placeholder IDs.
- Placeholder summary key/string only for structured testing, not final copy.

Not allowed:
- Tactical resolution logic.
- Direct mutation of strategic state from DTOs.

## Dependencies

- Required prior stories:
  - STORY-STRAT-001 scenario/map graph state.
- Required architecture decisions:
  - Approved Unity technical scheme, control manifest, testing strategy, and CI/build automation.
- Required tactical design:
  - Strategic-map §14 is the binding source for this DTO story. Tactical GDD compatibility should be checked, but unresolved draft tactical combat details must not block the DTO minimum unless they contradict §14. Codex must not implement tactical combat internals from draft tactical sources.

## Acceptance criteria

- [ ] Given valid attacker and defender side snapshots, when a BattleSetup DTO is created/validated for a guarded site, then it contains battle ID, scenario/source/site/node IDs, battle type, faction/controller IDs, attacking army snapshot, defending guard army snapshot, tactical objective ID placeholder if supplied, and no direct strategic runtime mutation hooks.
- [ ] Given valid faction-vs-faction side snapshots, when a BattleSetup DTO is created/validated for a site contest, then it contains both faction/champion references and HumanLocal/CombatAI controller assignments as data.
- [ ] Given missing battle ID, side, controller, or army snapshot, when validation runs, then it fails with clear diagnostics.
- [ ] Given a BattleResult with a matching battle ID and valid outcome, when validation runs, then it is accepted as a result payload without applying strategic consequences.
- [ ] Given a BattleResult with mismatched battle ID, invalid outcome, or missing army result, when validation runs, then it fails with clear diagnostics.
- [ ] Given DTO creation from strategic army state, when the source strategic army is later changed in the test, then the DTO snapshot remains unchanged.
- [ ] Domain DTO code compiles without UnityEngine, MonoBehaviour, ScriptableObject, scene, prefab, input, camera, or UI references.

## Verification requirements

- Unit tests: N/A unless a non-Unity pure C# runner exists.
- Unity edit-mode tests: Required for DTO validation, snapshot/copy behavior, setup/result ID matching, and invalid diagnostics.
- Unity play-mode tests: N/A; no scene/prefab/UI behavior is authorized.
- Integration/data validation tests: N/A beyond domain/EditMode contract tests.
- Manual Unity scene/prefab checks: N/A.
- Screenshot/video evidence: N/A.
- Performance budget or N/A: N/A for small DTO validation.
- CI evidence: Required on implementation PR.
- Playtest evidence: N/A.
- TDD evidence required? Yes.
- Automation deferred? No.

## Ambiguity Check

Status: PASS.

Open questions:
- None for the minimum DTO contract. Tactical combat internals remain deliberately out of scope.

Assumptions:
- DTO shape follows strategic-map §14 even if tactical combat internals evolve later.
- Army snapshots can reuse or copy existing STORY-STRAT-001 army runtime/stack state shapes unless an equivalent pure DTO copy is cleaner.

Out of scope:
- Same as story Out of scope section.

Allowed stubs/mocks:
- Same as Allowed stubs section.

Human-approved exceptions:
- None.

## Branch / PR requirements

- Branch name: `story/STORY-TAC-001-battle-setup-result-dto-contracts`
- PR title: `STORY-TAC-001 Battle setup result DTO contracts`
- Required linked story ID: `STORY-TAC-001`
- Required linked GDD/ADR/control docs:
  - `design/gdd/strategic-map.md` §§6, 7, 10, 12, 14.
  - `design/gdd/tactical-combat.md` only for compatibility check, not extra implementation scope.
  - `docs/architecture/control-manifest.md` §§1, 2, 4, 5, 6, 7, 9, 10.
  - `docs/architecture/testing-strategy.md` and `docs/architecture/ci-build-automation.md`.
- Required root/scoped AGENTS.md instructions: Unity repo root `AGENTS.md` and scoped source/test `AGENTS.md` under touched paths.
- Required evidence summary: RED/GREEN TDD summary, DTO tests added/changed, CI link/status, omissions section.

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
- [ ] Human approval has been given or delegated gate approval is recorded.

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

READY-candidate. Gate blockers: human approval pending.
