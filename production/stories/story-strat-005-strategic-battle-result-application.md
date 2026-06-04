---
title: STORY-STRAT-005 Strategic Battle Result Application
type: story
status: draft
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
    production/stories/story-strat-004-site-interaction-and-guarded-battle-trigger,
    production/stories/story-tac-001-battle-setup-result-dto-contracts,
  ]
approval: pending
---

# Story: STORY-STRAT-005 Strategic Battle Result Application

## Status

Draft. Direction clarified on 2026-06-04: winning a guarded neutral-site battle should immediately control the site. It remains not READY until STORY-STRAT-004 is approved/merged and reward/victory defaults are finalized.

## Story type

Logic + Integration.

## Estimate

- Size: M/L.
- Basis: applies `BattleResult` to Champion armies, guard state, site control/reward eligibility, and victory checks. This is larger than STORY-STRAT-004 because it touches several strategic state concepts.

## Parent epic

- Epic ID/path: `production/epics/epic-strat-mvp-001-strategic-mvp-core-loop.md`.

## User/player/system value

As a player, I want tactical battle results to visibly and deterministically change the strategic map, so that guarded-site battles become meaningful strategic decisions instead of disconnected DTO handoffs.

## Source requirements

Exact source references:

- GDD path + section/rule:
  - `design/gdd/strategic-map.md` §6 Core Loop Contract, steps 7-9.
  - `design/gdd/strategic-map.md` §10 Site and Infrastructure States, ownership/control contract rules 1-6.
  - `design/gdd/strategic-map.md` §11 Resources, Intel, and Recruitment/Reinforcement Minimum, resource/reward contract rules 1-8.
  - `design/gdd/strategic-map.md` §12 Champion/Army Strategic State and Movement Allowance, army strategic state rules 2-5 and movement/interaction contract rules 6-7.
  - `design/gdd/strategic-map.md` §13 Turn/Scenario/Victory Structure, champion defeat contract and objective control contract.
  - `design/gdd/strategic-map.md` §14 Strategy-to-Tactical DTOs, BattleResult minimum, strategic application contract, and minimum strategic loop test cases 2-6.
- ADR / architecture section / control-manifest rule:
  - `docs/architecture/unity-technical-scheme.md` — domain logic separated from Unity presentation.
  - `docs/architecture/control-manifest.md` §§1, 2, 4, 5, 6, 7, 9, 10.
  - `docs/architecture/testing-strategy.md` — TDD and story evidence requirements.
  - `docs/architecture/ci-build-automation.md` — CI evidence requirements.
- UX/content/art/worldbuilding:
  - No final result-summary copy. Placeholder summary keys and structured facts only.
- Parent epic:
  - `production/epics/epic-strat-mvp-001-strategic-mvp-core-loop.md`.

## In scope

Concrete implementation tasks authorized by this story:

- Add or extend a strategic battle-result application service/command that consumes a valid `BattleResult` for a pending/unresolved battle created by STORY-STRAT-004.
- Validate battle ID, source site/node, expected battle type, required side results, and unresolved battle state before applying.
- Apply attacker and defender army survivor/loss data back to strategic Champion/guard/site state.
- For guarded neutral sites:
  - attacker win clears guards;
  - attacker win makes site claim/reward eligible or controlled according to the approved default;
  - defender win leaves guards active and does not grant rewards;
  - invalid/mismatched/cancelled results do not silently mutate strategic state.
- Apply guarded neutral-site attacker-win control immediately.
- Apply one-time guarded-site rewards immediately on attacker win if resource stockpiles already exist; otherwise mark reward application as explicitly deferred without inventing hidden economy behavior.
- Evaluate only-Champion defeat and scenario victory when the battle result defeats a faction's only Champion.
- Emit a structured strategic result summary suitable for a later UI layer.
- Add tests for attacker win, defender/guard win, invalid result, duplicate application, reward/control consequences, and Champion defeat victory.

## Out of scope

Adjacent behavior not authorized by this story:

- Tactical combat execution, tactical scene, battle simulation, AI, animation, tactical UI, or fake tactical gameplay.
- Full recruitment/reinforcement UI or offer purchase flow.
- Recurring income timing unless already supported and necessary for existing reward structures.
- Enemy-controlled site contests unless explicitly promoted before READY.
- Central objective hold victory UI unless existing state can be tested domain-only.
- Full save/load, campaign persistence, strategic AI, networking, fog/feed misinformation, final copy/art/audio.
- Deep casualty recovery, retreats, wounded bodies, Echo continuation, clinics, or replacement Champion systems.

## Allowed stubs, mocks, placeholders, or temporary data

Allowed:

- Test-local `BattleSetup`/`BattleResult` payloads matching STORY-TAC-001.
- Test-local guarded resource site and neutral guard army fixtures.
- Placeholder structured result summary keys/facts.
- A minimal reward delta using existing resource IDs if resource stockpiles already exist; otherwise reward eligibility may be represented as an explicit deferred marker.

Not allowed:

- Tactical battle resolver that fabricates gameplay outcomes as production behavior.
- Direct tactical mutation of strategic state.
- Unapproved final economy/resource expansion beyond Credits/Materials/Intel.

## Dependencies

- Required prior stories:
  - STORY-TAC-001 battle setup/result DTO contracts.
  - STORY-STRAT-004 site interaction and guarded battle trigger.
- Required architecture decisions:
  - Approved Unity technical scheme, control manifest, testing strategy, and CI/build automation.
- Required Unity/package setup:
  - Existing Unity project and CI from SPIKE-001.

## Acceptance criteria

- [ ] Given a pending guarded-site battle and an attacker-win `BattleResult` with matching battle ID, when the strategy layer applies the result, then attacking Champion army survivors/losses are updated from the result, guard state is cleared/defeated, and the site immediately becomes controlled by the attacking faction.
- [ ] Given a pending guarded-site battle and a defender-win `BattleResult`, when the result is applied, then attacking Champion army survivors/losses are updated, guards remain active if surviving, no site reward/control is granted, and the pending battle is closed or marked resolved.
- [ ] Given a mismatched battle ID, missing side result, invalid source site, or already-resolved battle, when result application is attempted, then validation fails with clear diagnostics and no strategic state mutation occurs.
- [ ] Given an attacker-win guarded-site result with reward eligibility enabled, when result application succeeds, then Credits/Materials/Intel deltas are applied immediately if stockpiles exist, or explicitly marked deferred without changing hidden economy state.
- [ ] Given a result that defeats the opposing faction's only Champion, when result application completes, then scenario victory/loss state is set according to the champion defeat contract.
- [ ] Given any applied battle result, tactical DTOs remain input payloads only; site control, rewards, Champion state, and victory changes occur only inside strategic result application.

## Verification requirements

- Unit tests: N/A unless a non-Unity pure C# runner exists.
- Unity edit-mode tests: Required for result validation, mutation/no-mutation behavior, army loss application, guard clearing, reward/control default, Champion defeat victory, duplicate application, and diagnostics.
- Unity play-mode tests: Optional/N/A unless a minimal UI smoke path exists after STORY-STRAT-004.
- Integration/data validation tests: Required if implementation adds serialized fixtures or validators.
- Manual Unity scene/prefab checks: N/A unless implementation touches scene/presentation.
- Screenshot/video evidence: N/A unless implementation touches scene/presentation.
- Performance budget or N/A: N/A for small domain state transition.
- CI evidence: Required on implementation PR.
- Playtest evidence: N/A.
- TDD evidence required? Yes.
- Automation deferred? No.

If a verification type is N/A, the PR must say why.

## Ambiguity Check

Status: NEEDS FINAL APPROVAL.

Resolved by user on 2026-06-04:

- On neutral guarded-site attacker win, control is automatic: win battle, site controlled.

Recommended defaults for approval:

- One-time rewards apply immediately on attacker win if resource stockpiles exist; if not, result summary says reward application is deferred rather than inventing economy behavior.
- Champion defeat should set explicit defeated state now, but full scenario victory should be included only if the existing scenario victory state can support it cleanly.
- Enemy-controlled site contests should be separate `STORY-STRAT-006`, not bundled into this guarded-neutral-site slice.

Open questions:

- Approve the three recommended defaults above?

Assumptions:

- Default: attacker win against a neutral guarded resource site clears guards and controls the site in one strategic result application.

Out of scope:

- Same as story Out of scope section.

Allowed stubs/mocks:

- Same as Allowed stubs section.

Human-approved exceptions:

- None.

If status is FAIL, this story is not READY.

## Branch / PR requirements

- Branch name: `story/STORY-STRAT-005-strategic-battle-result-application`
- PR title: `STORY-STRAT-005 Strategic battle result application`
- Required linked story ID: `STORY-STRAT-005`
- Required linked GDD/ADR/control docs:
  - `design/gdd/strategic-map.md` §§6, 10, 11, 12, 13, 14.
  - `docs/architecture/control-manifest.md` §§1, 2, 4, 5, 6, 7, 9, 10.
  - `docs/architecture/testing-strategy.md` and `docs/architecture/ci-build-automation.md`.
- Required root/scoped AGENTS.md instructions: Unity repo root `AGENTS.md` and scoped source/test `AGENTS.md` under touched paths.
- Required evidence summary: RED/GREEN TDD summary, result application tests, mutation/no-mutation evidence, CI link/status, omissions section.

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
- [ ] Ambiguity Check status is PASS.
- [x] Branch / PR / CI traceability requirements are stated.
- [ ] Human approval has been given or delegated gate approval is recorded.

## DONE gate

- [ ] Implementation matches approved story scope.
- [ ] Acceptance criteria pass.
- [ ] Required verification evidence exists.
- [ ] Required automated tests, validators, and PlayMode/smoke evidence pass, or human-approved exceptions are documented.
- [ ] No unauthorized design or architecture decisions were introduced.
- [ ] Omissions/stubs/mocks/deferred work are explicitly documented.
- [ ] PR/code review is complete.
- [ ] CI passes or human-approved exceptions are documented.
- [ ] Required docs were updated in the correct source-of-truth layer.

## Verdict

Draft.
