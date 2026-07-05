---
title: EPIC-VSLICE-MVP-015 Post-Audit Foundation Pivot and Reconciliation
type: epic
status: approved
phase: production
owner: shared
created: 2026-07-03
updated: 2026-07-05
source_lore: []
related:
  [
    production/planning/post-audit-foundation-pivot-2026-07-03,
    docs/architecture/data-scenario-save-format-adr,
    docs/architecture/data-authoring-options,
    docs/architecture/control-manifest,
    docs/architecture/testing-strategy,
    docs/architecture/ci-build-automation,
    design/gdd/strategic-map,
    design/gdd/tactical-combat,
    design/gdd/game-pillars,
    design/registry/entities,
    design/registry/formulas,
    design/registry/terms,
    production/stories/story-data-001-static-scenario-data-contract-and-scenario-extraction-prep,
    production/stories/story-playtest-001-playtest-journal-and-gate-hook,
    production/stories/story-gate-001-hollow-gate-and-source-truth-reconciliation,
    production/stories/story-determinism-001-determinism-and-rng-decision-record,
  ]
approval: approved
---

# EPIC-VSLICE-MVP-015 Post-Audit Foundation Pivot and Reconciliation

## Status

APPROVED / active fourth child READY. Human approval recorded 2026-07-03: "Approved" for the post-audit mini-epic recommended after the full three-repo audit. `STORY-DATA-001` merged 2026-07-05 through Unity PR #138, proving the first data/scenario extraction slice. `STORY-PLAYTEST-001` merged 2026-07-05 through game-design PR #1, creating the journal/gate hook. `STORY-GATE-001` merged 2026-07-05 through game-design PR #2, creating the hollow-gate reconciliation report and rule hooks. `STORY-DETERMINISM-001` is now READY / approved as the next design/control packet; no Unity runtime implementation task is active until a later child story is promoted and the Unity pointer is updated.

This epic is not direct Unity implementation authority. Agents and Codex may only implement READY child stories.

## Capability goal

Convert the 2026-07-02 full-project audit into enforceable production behavior: data/scenario authority, playtest/fun evidence, deterministic design stance, honest gates, and source-of-truth reconciliation.

## Player / design value

As a designer/player-tester, I need the project to stop accumulating hollow scaffolding and start proving Neon Champions' differentiators, so future implementation tests the actual game rather than only a generic HoMM-like loop.

Relevant pillars:

- Intel as secrets turned into power.
- Dirty information and source-tagged uncertainty.
- Infrastructure-first conflict.
- Champions as legitimacy and public force projection.
- HoMM-like exploration/capture/tactics, but not as mere reskin.

## Source requirements

- `production/planning/post-audit-foundation-pivot-2026-07-03.md` — approved direction and scope guard.
- `docs/architecture/data-authoring-options.md` — approved phased-hybrid data authoring direction.
- `docs/architecture/data-scenario-save-format-adr.md` — post-audit data/scenario/save ADR.
- `docs/architecture/control-manifest.md`, `testing-strategy.md`, and `ci-build-automation.md`.
- `design/gdd/game-pillars.md`, `strategic-map.md`, and `tactical-combat.md`.
- Existing Unity implementation state, especially hardcoded scenario construction and serializable runtime/domain state.

## Scope

### In scope

- A thin ADR locking static definition / scenario data / runtime state / save data boundaries.
- A first scenario-data contract and extraction prep story for the current playable scenario.
- A playtest journal artifact and gate hook.
- A determinism decision record: deterministic-by-default vs seeded RNG service.
- Hollow-gate reconciliation: placeholder validator, empty registry, empty bridge templates, status drift, and draft-source exceptions.
- A dumb strategic AI story plan for later single-player-valid playtesting.

### Out of scope

- Full scenario/map editor.
- Full save/load UI or campaign persistence.
- Sophisticated strategic AI.
- Full dirty-information/fog/PR/counter-intel implementation.
- Broad tactical redesign or balance pass.
- World-repo canon approvals beyond recording design-facing dependencies.
- Final art/audio/VFX/icons/localization/accessibility.

## Child stories

Agents and Codex may not implement this epic directly. They may only implement READY child stories.

| Story | Status | Type | Depends On | Evidence |
| --- | --- | --- | --- | --- |
| [STORY-DATA-001 Static/Scenario Data Contract and Scenario Extraction Prep](../stories/story-data-001-static-scenario-data-contract-and-scenario-extraction-prep.md) | DONE / merged | Config/Data + Architecture | EPIC-014 complete; this epic; data/scenario/save ADR | Unity PR #138 merged; post-merge CI passed |
| [STORY-PLAYTEST-001 Playtest Journal and Gate Hook](../stories/story-playtest-001-playtest-journal-and-gate-hook.md) | DONE / merged | Playtest + Process | This epic; DATA-001 merged | Game-design PR #1 merged; publish CI passed |
| [STORY-GATE-001 Hollow Gate and Source-Truth Reconciliation](../stories/story-gate-001-hollow-gate-and-source-truth-reconciliation.md) | DONE / merged | Process/Tooling | This epic; PLAYTEST-001 merged | Game-design PR #2 merged; publish CI passed |
| [STORY-DETERMINISM-001 Determinism and RNG Decision Record](../stories/story-determinism-001-determinism-and-rng-decision-record.md) | READY / approved | Architecture/Design | This epic; data/scenario/save ADR; testing strategy | Runnable prompt `production/sprints/codex-story-determinism-001.prompt.txt` |
| STORY-AI-001 Dumb Strategic AI Playtest Opponent | Draft | Logic/AI | Data/scenario contract preferred; determinism ADR preferred | Future story |

Allowed story statuses: Draft, NEEDS WORK, READY-candidate, READY, IN PROGRESS, REVIEW, DONE, BLOCKED.

## Risks

| Risk | Type | Impact | Mitigation |
| --- | --- | --- | --- |
| Pivot becomes broad cleanup swamp | Scope | No playable progress | Keep child stories thin and acceptance-driven |
| ADR pretends future editor/save details are solved | Architecture | Locks bad design early | Decide only boundaries and first data contract |
| Scenario extraction changes gameplay | Testing | Invalidates current playtest baseline | Require no gameplay change and regression smoke |
| Gate cleanup becomes ceremony | Process | More hollow scaffolding | Every gate must be able to fail or be deleted/demoted |
| Current READY Unity task conflicts with pivot | Production | Two active implementation packets | This epic does not alter Unity pointer until a child story is promoted and pointer is updated |

## Epic readiness gate

- [x] Capability goal is clear.
- [x] Audit-derived source requirements are explicit.
- [x] Scope and out-of-scope are bounded.
- [x] Child stories are identified.
- [x] First implementation-facing story promoted to READY after EPIC-014 completion; sequencing decision satisfied.
- [x] Required test/evidence layers are known.
- [x] No Unity implementation is authorized by the epic alone.

## Epic DONE gate

- [ ] Data/scenario/save ADR is accepted or replaced.
- [x] Current scenario has a data contract/extraction path or a documented blocker.
- [x] Playtest journal exists and is referenced by future closeout gates.
- [ ] Determinism decision is recorded.
- [x] Hollow-gate/source-truth reconciliation report exists and at least one hollow control surface is filled/demoted/deleted.
- [ ] Follow-up implementation stories are created only where needed.

## Verdict

APPROVED / active fourth child READY. `STORY-DATA-001`, `STORY-PLAYTEST-001`, and `STORY-GATE-001` are DONE / merged. Execute next only through READY child stories; `STORY-DETERMINISM-001` is the current approved design/control packet and does not authorize Unity runtime changes.
