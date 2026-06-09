---
title: STORY-QA-003 Loop Slice Visual Readability and Clickable Layout Pass
type: story
status: ready-candidate
phase: production
owner: shared
created: 2026-06-09
updated: 2026-06-09
source_lore: []
related:
  [
    design/gdd/strategic-map,
    design/gdd/tactical-combat,
    docs/architecture/control-manifest,
    docs/architecture/testing-strategy,
    docs/architecture/ci-build-automation,
    production/epics/epic-vslice-mvp-002-larger-map-bases-recruitment-minimal-tactical-combat,
    production/stories/story-loop-003-larger-map-recruitment-and-neutral-capture-vertical-slice,
    production/stories/story-qa-001-strategic-smoke-cleanup-readability-bugfix-pass,
    production/stories/story-qa-002-strategic-map-readability-actor-clarity-fix-pass,
  ]
approval: pending
---

# Story: STORY-QA-003 Loop Slice Visual Readability and Clickable Layout Pass

## Status

READY-candidate / approval pending. Drafted after `STORY-LOOP-003` merged and proved the connected recruitment-to-capture loop, but human review flagged the current visual layer as too hard to read and interact with: BMP evidence is difficult to parse, layout does not use the screen well, buttons/controls need to be clearer and clickable, and all views should open and function cleanly.

This packet is intentionally a visual/readability pass over the existing connected slice, not a new gameplay-system packet.

## Story type

QA + UI/UX Readability + Visual/Feel + Interaction Regression.

## Estimate

- Size: M.
- Basis: likely touches existing placeholder strategic/tactical presentation, layout constants/helpers, click/input hit areas, PlayMode evidence capture, and tests. It should not require new gameplay rules.

## Parent epic

- Epic ID/path: `production/epics/epic-vslice-mvp-002-larger-map-bases-recruitment-minimal-tactical-combat.md`.

## User/player/system value

As a human tester of the MVP loop slice, I need the strategic map, recruitment view, tactical view, and post-capture/result feedback to be readable, scalable, and interactable at the target screen size, so I can judge the loop itself instead of fighting cramped placeholder UI and unclear controls.

## Source requirements

- `design/gdd/strategic-map.md` §§2, 6, 8, 9, 10, 11, 12, 14.
- `design/gdd/tactical-combat.md` MVP visual/handoff/control sections already implemented by prior tactical stories.
- `docs/architecture/control-manifest.md` §§1, 2, 4, 5, 6, 7, 9, 10.
- `docs/architecture/testing-strategy.md`.
- `docs/architecture/ci-build-automation.md`.
- Prior QA/readability packets: `STORY-QA-001`, `STORY-QA-002`.
- Immediate baseline: Unity PR #24 / `STORY-LOOP-003` evidence under `production/evidence/STORY-LOOP-003/`.

## Problem statement / observed issues

Human review after LOOP-003:

- Current BMP evidence/screens are hard to read.
- Current placeholder layout is hard to interact with.
- Controls/buttons should be clearer and reliably clickable.
- The UI should use more of the screen instead of crowding into cramped areas.
- Layout should scale with the screen/evidence resolution.
- Strategic, recruitment, tactical, and result views should all open properly and remain functional.

## In scope

### Baseline / audit

- Start from Unity `main` after `STORY-LOOP-003` merge.
- Capture or preserve baseline LOOP-003 screenshots for comparison.
- Audit the connected path screens:
  - strategic map / HUD initial state;
  - Champion selection and reachable-route state;
  - recruitment offer preview and apply state;
  - guarded-site preview / tactical launch;
  - tactical board controls/state;
  - post-capture strategic result.

### Layout/readability improvements

- Rework placeholder layout so important views use more of the 1280x720 evidence frame and scale with the screen where feasible.
- Improve separation and hierarchy for:
  - active actor/faction/controller/Champion/resources;
  - selected Champion/army/reachable routes;
  - recruitment offers and apply controls;
  - site interaction controls;
  - tactical mode board, current stack, legal actions, and feedback;
  - post-capture/result feedback.
- Reduce or eliminate overlapping/crowded labels at the default evidence resolution.
- Improve placeholder contrast, text size, panel/zone grouping, and spacing where directly tied to readability.
- Keep raw IDs acceptable for debug/prototype evidence, but arrange them so the screen can be read at a glance.

### Clickability / interaction clarity

- Make all currently implemented controls visibly clear and clickable through existing public input/application paths:
  - End Turn;
  - Champion selection;
  - route/node movement selection where implemented;
  - site interaction / attack / recruitment affordances;
  - recruitment offer controls;
  - tactical move/attack/pass/wait/defend controls where currently implemented.
- Add or update PlayMode checks that controls/views are present and can be activated without relying on hidden test-only state mutation.
- If the current implementation lacks a public clickable affordance for a view that already opens through a test/helper method, add the narrowest placeholder clickable control needed to open it, without adding new gameplay rules.

### Evidence

- Add evidence under `production/evidence/STORY-QA-003/README.md`.
- Include before/after screenshots for the same or comparable moments:
  - strategic map initial/selected state;
  - recruitment preview/apply;
  - tactical handoff/control state;
  - post-capture result.
- Include a checklist that directly answers the human complaints above.

## Out of scope

- New gameplay mechanics, economy/base/town production, new recruitment offers/sites, strategic AI, save/load, final map content, final names, final balance, or enemy-faction contests.
- New tactical mechanics, abilities, initiative redesign, tactical AI, combat balance, new unit content, or full deployment UI.
- Final UI art direction, animation, audio, VFX polish, UI Toolkit/Canvas architecture migration, localization system, new packages, render pipeline changes, or final accessibility pass.
- Rewriting architecture or moving gameplay rules into presentation code.
- Pixel-perfect final UI; this remains a prototype readability pass.

## Allowed stubs, mocks, placeholders, or temporary data

Allowed:

- Existing placeholder IDs/display keys.
- Primitive shapes, debug panels, TextMesh labels, simple colors, simple hit boxes/buttons, simple layout helpers.
- Existing screenshot/evidence capture mechanism.

Not allowed:

- Fake screenshots or evidence that bypass runtime/domain/application paths.
- Presentation code directly mutating canonical gameplay state.
- Hidden implementation of deferred gameplay systems.
- New final UI/lore/content decisions.

## Dependencies

- Required prior stories:
  - `STORY-LOOP-003` DONE / merged in Unity PR #24.
  - `STORY-TAC-006`, `STORY-STRAT-006`, `STORY-MAP-001`, `STORY-TAC-005` DONE / merged.
  - Prior QA layout precedents `STORY-QA-001` and `STORY-QA-002`.
- Required assets/data:
  - Existing deterministic larger-map and tactical placeholder data.
- Required architecture decisions:
  - Current Unity data/runtime/presentation boundaries remain binding.

## Acceptance criteria

- [ ] Given the connected loop starts at the target/default evidence resolution, the strategic map/HUD uses the screen coherently and key labels are readable without console logs.
- [ ] Given the active Champion is selected, reachable route/node information is visible without hiding the map topology or active actor state.
- [ ] Given the recruitment site is selected, both offers and their action controls are readable, spatially separated, and clickable.
- [ ] Given a recruitment offer is applied, the resource, stock, army, and feedback changes are visible in a cleaner layout.
- [ ] Given a guarded-site interaction is available, the attack/site interaction control is clear, clickable, and does not overlap other controls.
- [ ] Given tactical mode opens, the tactical board, current stack, available controls, and feedback are readable and use more of the screen.
- [ ] Given tactical controls are used, existing move/attack/pass/wait/defend controls remain functional through public input/application paths.
- [ ] Given the battle resolves, the post-capture strategic result view opens and clearly communicates capture/guard/reward-deferred status.
- [ ] Existing LOOP-003 connected PlayMode smoke still passes.
- [ ] Before/after screenshot evidence demonstrates improved readability and clickability.
- [ ] CI passes.

## Verification requirements

- Unity EditMode tests: Required for any pure layout helper or hit-target calculation logic added.
- Unity PlayMode tests: Required for connected-loop regression and control/view activation coverage where feasible.
- Manual Unity scene/prefab checks: Required if scene/prefab assets change; prefer code-driven placeholder layout if feasible.
- Screenshot/video evidence: Required before/after screenshots for strategic, recruitment, tactical, and result views. Video optional but useful if clickability is hard to convey.
- CI evidence: Required on PR branch and post-merge main.
- TDD evidence required? Yes for helper logic or input/clickability regressions; PlayMode/manual evidence for presentation-only layout changes.
- Performance budget: N/A, but avoid expensive effects or new rendering systems.

## Ambiguity Check

Status: NEEDS APPROVAL.

Resolved user direction, 2026-06-09:

- Next slice should be a visual/readability pass.
- Current BMP/layout evidence is hard to read.
- Current layout is hard to interact with.
- Buttons should be clear and clickable.
- Layout should be cleaner, scale with the screen, and use more of the screen.
- All views should properly open and remain functional.

Open approval item:

- Human must approve this exact packet as READY before Codex runs it.

Assumptions:

- Placeholder UI is acceptable; final art/UI architecture is not required.
- Scope can include narrow clickable placeholder controls for already-implemented actions/views, but not new gameplay systems.

## Branch / PR requirements

- Branch name: `story/STORY-QA-003-loop-slice-visual-readability-clickable-layout`
- PR title: `STORY-QA-003 Loop slice visual readability and clickable layout pass`
- Required linked story ID: `STORY-QA-003`
- Required evidence summary: user-observed issues, before/after screenshots, changed files, tests/checks, CI, remaining UX debt.
- Required omissions section: no final UI/art, no new gameplay systems, no tactical mechanics expansion, no save/load, no content/balance expansion.

PR must explicitly list known omissions, stubs, mocks, assumptions, deferred work, or state `No known omissions`.

## Story readiness gate

- [x] Story has stable ID, title, type, status, and parent epic.
- [x] User/player/system value is clear.
- [x] Exact GDD source sections are linked.
- [x] Exact ADR/architecture/control-manifest sources are linked.
- [x] Relevant root/scoped AGENTS.md instructions are identified.
- [x] UX/content/art/worldbuilding references are linked if relevant or explicitly N/A.
- [x] In-scope work is concrete and bounded.
- [x] Out-of-scope work is explicit.
- [x] Stubs/mocks/placeholders are explicitly listed.
- [x] Dependencies are listed.
- [x] Acceptance criteria are observable and testable.
- [x] Verification requirements are defined according to `docs/architecture/testing-strategy.md`.
- [x] Required automated tests/validators/PlayMode evidence are listed.
- [ ] Ambiguity Check status is PASS.
- [x] Branch / PR / CI traceability requirements are stated.
- [ ] Human approval has been given or delegated gate approval is recorded.

## DONE gate

A story may be marked DONE only when all items are true:

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

READY-candidate. Strongly recommended next slice after LOOP-003, but not implementation-authorized until human approval promotes it to READY.
