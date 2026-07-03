---
title: STORY-DATA-001 Static/Scenario Data Contract and Scenario Extraction Prep
type: story
status: ready-candidate
phase: production
owner: shared
created: 2026-07-03
updated: 2026-07-03
source_lore: []
related:
  [
    production/epics/epic-vslice-mvp-015-post-audit-foundation-pivot-and-reconciliation,
    production/planning/post-audit-foundation-pivot-2026-07-03,
    docs/architecture/data-scenario-save-format-adr,
    docs/architecture/data-authoring-options,
    docs/architecture/control-manifest,
    docs/architecture/testing-strategy,
    docs/architecture/ci-build-automation,
  ]
approval: approved
---

# STORY-DATA-001 Static/Scenario Data Contract and Scenario Extraction Prep

## Status

READY-candidate / approved and queued after current epic. Human approval recorded 2026-07-03: "Okay prepare next story and approve." Human sequencing decision remains: wait until current EPIC-014 / `STORY-TAC-ROLE-001` completes, then pivot to EPIC-015 and promote this story for implementation. Unity implementation is not authorized until EPIC-014 is complete, this story is explicitly promoted to READY, and the Unity current-task pointer is updated.

## Story type

Config/Data + Architecture + Integration.

## Parent epic

- `production/epics/epic-vslice-mvp-015-post-audit-foundation-pivot-and-reconciliation.md`

## User/player/system value

As a designer/system, I want the current playable scenario represented by validated data instead of hardcoded C#, so future scenarios, balancing, save/load, validators, and dumb strategic AI do not multiply drift.

## Source requirements

- `docs/architecture/data-scenario-save-format-adr.md` — data/static/scenario/runtime/save boundaries and first extraction direction.
- `docs/architecture/data-authoring-options.md` — approved phased-hybrid data authoring requirements.
- `docs/architecture/control-manifest.md` — no hardcoded tunable gameplay values, engine boundary, stable IDs.
- `docs/architecture/testing-strategy.md` and `ci-build-automation.md`.
- Current Unity hardcoded scenario construction, especially `StrategicMapPresentationSmokeScenario` and related scenario/runtime factories.

## In scope

- Inspect current Unity scenario construction and define the smallest static/scenario data contract needed to represent the current playable scenario.
- Add one checked-in sample scenario data file for the current smoke/playable scenario.
- Add importer/converter code that creates the same domain/application definitions/runtime state currently created by code.
- Add validation for duplicate IDs, missing required fields, unknown references, empty/blank IDs, and basic numeric ranges used by the scenario.
- Add focused EditMode tests for valid load and invalid data rejection.
- Add PlayMode or smoke evidence that the current visible loop still works with the data-backed scenario.
- Keep old hardcoded factory path only as temporary fallback if needed, explicitly documented as deferred work.

## Out of scope

- Full map/scenario editor.
- Full save/load UI.
- Full conversion of every unit/faction/tactical/action/facility constant.
- New gameplay, map topology, balance, factions, sites, objectives, dirty-information, or AI behavior.
- ScriptableObject authoring UI.
- Localization framework completion.

## Allowed stubs, mocks, placeholders, or temporary data

- A minimal schema scoped to the current scenario is allowed.
- Temporary fallback to the existing C# scenario path is allowed only if documented and not used to bypass tests.
- JSON is the default text format; if Codex chooses another format, it must stop and request ADR update.

## Dependencies

- EPIC-015 approved.
- ADR approved.
- Unity README current-task pointer must name this story before implementation.
- Current `STORY-TAC-ROLE-001` / EPIC-014 must complete before this becomes the active Unity task. Human sequencing decision 2026-07-03: wait, then pivot to EPIC-015 and this story.

## Acceptance criteria

- [ ] The current playable scenario has a checked-in data representation reviewed in Git.
- [ ] Importer/converter creates runtime/domain state equivalent to the previous hardcoded scenario for the in-scope values.
- [ ] Validator rejects duplicate IDs, blank IDs, missing required fields, unknown references, and out-of-range numeric values covered by the schema.
- [ ] Existing visible strategic/tactical loop smokes are not intentionally changed.
- [ ] Evidence lists which values remain hardcoded and why.
- [ ] Placeholder Validator is either pointed at the new data validation path or a follow-up blocker is recorded.

## Verification requirements

- `git diff --check`.
- Focused EditMode importer/validator tests.
- Existing relevant scenario/domain tests updated only where the data path changes source construction.
- PlayMode smoke or generated evidence showing the current scenario still loads and is playable.
- Exact-head Unity Foundation CI before merge; post-merge main CI after merge.
- PR omissions section listing remaining hardcoded values / deferred schema coverage.

## Ambiguity Check

Status: PASS for approved READY-candidate, FAIL for implementation until EPIC-014 completes and this story is explicitly promoted to READY.

Resolved sequencing decision:

- Human decision 2026-07-03: do not supersede the currently READY `STORY-TAC-ROLE-001`; wait until the current epic completes, then pivot to EPIC-015 and this story.

Assumptions:

- JSON is acceptable as the first reviewable text data format.
- Current gameplay should remain unchanged.

Human-approved exceptions:

- This story is human-approved as the next post-EPIC-014 packet, but must wait until EPIC-014 completes and still requires explicit promotion to READY plus Unity current-task pointer update.

## Branch / PR requirements

- Branch name: `story/STORY-DATA-001-static-scenario-data-contract`
- PR title: `STORY-DATA-001 static scenario data contract and extraction prep`
- Required linked story ID: `STORY-DATA-001`.
- Required evidence path: `production/evidence/STORY-DATA-001/`.
- Codex must commit and push the implementation branch to remote, or clearly explain why it stopped without pushing.

## Story readiness gate

- [x] Story has stable ID, title, type, status, and parent epic.
- [x] User/system value is clear.
- [x] Exact ADR/architecture/control-manifest sources are linked.
- [x] In-scope work is concrete and bounded.
- [x] Out-of-scope work is explicit.
- [x] Verification requirements are defined.
- [x] Human approved this story as the queued next packet after EPIC-014.
- [ ] Unity current-task pointer is updated to this story.
- [x] Active task sequencing with `STORY-TAC-ROLE-001` is resolved: wait until EPIC-014 completes, then pivot.

## Guarded prompt

Prepared guarded prompt: `production/sprints/codex-story-data-001.prompt.txt`. It is not runnable until EPIC-014 completes, this story is promoted to `status: ready`, and the Unity README current-task pointer names `STORY-DATA-001`.

## Verdict

READY-candidate / approved and queued after EPIC-014.
