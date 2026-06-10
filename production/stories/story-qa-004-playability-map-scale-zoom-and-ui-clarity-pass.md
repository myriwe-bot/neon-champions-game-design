---
title: STORY-QA-004 Playability Map Scale, Zoom, and UI Clarity Pass
type: story
status: done
phase: production
owner: shared
created: 2026-06-10
updated: 2026-06-10
source_lore: []
related:
  [
    design/gdd/strategic-map,
    design/gdd/tactical-combat,
    docs/architecture/control-manifest,
    docs/architecture/testing-strategy,
    docs/architecture/ci-build-automation,
    production/epics/epic-vslice-mvp-002-larger-map-bases-recruitment-minimal-tactical-combat,
    production/stories/story-qa-003-loop-slice-visual-readability-and-clickable-layout-pass,
  ]
approval: approved
---

# Story: STORY-QA-004 Playability Map Scale, Zoom, and UI Clarity Pass

## Status

DONE. Unity PR #27 merged on 2026-06-10 as merge commit `d7661bf0e1fe7edca0704ac928994489e93ad337`; post-merge Unity `main` CI passed in run https://github.com/myriwe-bot/neon-champions-unity/actions/runs/27278547989.

Human visual review accepted the remediated result as satisfactory for now before merge. The implementation replaced the fragile world-space/debug control layout with runtime uGUI Canvas panels, layout groups, PNG evidence, deterministic marker separation, and clearer focus/action affordances while keeping the work within QA/playability scope.

## Story type

QA + UI/UX Readability + Visual/Feel + Interaction Regression + Playtest.

## Estimate

- Size: M/L.
- Basis: likely requires camera/map scaling or zoom, HUD/layout simplification, input feedback states, clearer button labeling, and screenshot/playtest evidence. It should not require new gameplay rules.

## Parent epic

- Epic ID/path: `production/epics/epic-vslice-mvp-002-larger-map-bases-recruitment-minimal-tactical-combat.md`.

## User/player/system value

As a human tester of the MVP vertical slice, I need the map, text, controls, click feedback, and tactical/strategic action affordances to be readable and understandable, so I can judge the prototype as a game instead of fighting tiny scale, overlapping labels, and unclear buttons.

## Source requirements

- `design/gdd/strategic-map.md` §§2, 6, 8, 9, 10, 11, 12, 14.
- `design/gdd/tactical-combat.md` MVP visual/handoff/control sections already implemented by prior tactical stories.
- `docs/architecture/control-manifest.md` §§1, 2, 4, 5, 6, 7, 9, 10.
- `docs/architecture/testing-strategy.md`.
- `docs/architecture/ci-build-automation.md`.
- Parent epic: `EPIC-VSLICE-MVP-002`.
- Immediate baseline: Unity `main` after PR #26 / commit `08802ad45b415aac525114bc1ab3629dc3842b35`.

## Problem statement / observed issues

Human closeout review after PR #26:

- The strategic map is still tiny and unreadable.
- Text labels overlap themselves.
- Buttons are obstructed by text.
- The prototype is very confusing.
- There is no zoom.
- It is hard to understand what is clicked.
- It is hard to understand what buttons do.
- Prior tactical move/attack fixes are not sufficient if the player cannot clearly read targets, actions, or feedback.

## In scope

### Baseline audit

- Start from Unity `main` after PR #26.
- Capture current baseline screenshots at the target evidence resolution before changes.
- Audit the whole connected slice for map scale, text overlap, button obstruction, selected/clicked feedback, and button meaning.

### Map scale and zoom / focus

- Make the strategic map substantially larger and easier to read at the default evidence resolution.
- Add a narrow prototype zoom/focus affordance if needed for readability. Acceptable forms include camera zoom buttons, scroll-wheel zoom, keyboard zoom, or a focused selected-site/selected-node view.
- Ensure zoom/focus does not hide required HUD/action state or break click targets.

### Text and button layout

- Remove or sharply reduce overlapping TextMesh/label clutter.
- Separate button text from world labels so buttons are not obstructed by labels.
- Prefer fewer, larger, clearer labels over many raw debug labels.
- Use concise action labels with explicit verbs, e.g. `Select`, `Move`, `Recruit`, `Attack`, `End Turn`, `Pass`, `Wait`, `Defend`.
- Keep raw IDs available only where useful for debug evidence; do not let IDs dominate the playable view.

### Click/action feedback

- Clearly show what is currently selected/clicked.
- Clearly show which actions are available for the selected thing.
- Clearly show whether an action succeeded or was invalid.
- Make tactical move/attack targets visually distinct enough that a tester can tell what can be moved to or attacked.

### Evidence and regression coverage

- Add or update PlayMode checks for map zoom/focus affordance, visible selection feedback, and non-overlapping/available action groups where feasible.
- Add manual screenshot/video evidence under `production/evidence/STORY-QA-004/` showing before/after:
  - initial strategic map readability;
  - selected Champion/site/node state;
  - recruitment action area;
  - tactical move/attack target state;
  - post-action feedback.
- Add a short human-facing checklist that directly answers every observed issue above.

## Out of scope

- New gameplay systems, victory conditions, strategic AI, save/load, final map content, final names, final UI art, animation, audio, VFX, balance, economy expansion, new recruitment systems, new tactical abilities, or final accessibility pass.
- UI Toolkit/Canvas architecture migration unless the implementer proves a tiny local change is lower risk than continuing the current placeholder path.
- Rewriting gameplay rules or moving domain/application state mutation into presentation code.
- Hiding labels/buttons instead of making the playable information understandable.

## Allowed stubs, mocks, placeholders, or temporary data

Allowed:

- Existing placeholder IDs/display keys where needed for debugging.
- Primitive panels, larger hit boxes, simple zoom/focus controls, simple color/highlight states, simple TextMesh labels, simple line/marker changes.
- Temporary prototype layout helpers if tested or covered by PlayMode evidence.

Not allowed:

- Fake screenshots or evidence that bypass runtime/application paths.
- Presentation code directly mutating canonical gameplay state.
- New final content/lore/UI decisions.

## Dependencies

- Required prior stories:
  - `STORY-QA-003` DONE / merged.
  - Hotfix PR #26 merged on Unity main.
  - All prior EPIC-VSLICE-MVP-002 child stories DONE / merged.
- Required data/assets:
  - Existing deterministic larger-map and tactical placeholder data.
- Required architecture decisions:
  - Current Unity data/runtime/presentation boundaries remain binding.

## Acceptance criteria

- [ ] Given the prototype starts at the target/default evidence resolution, the strategic map is large enough to read and judge without zooming the browser/image externally.
- [ ] Given map labels are visible, labels do not overlap themselves or obstruct primary action buttons at the default evidence resolution.
- [ ] Given the tester clicks/selects a Champion, site, route/node, tactical stack, or tactical target, the selected/clicked object is visibly identified.
- [ ] Given an action is available, its button/control uses a clear verb label and is not hidden under map/text labels.
- [ ] Given an action is unavailable or invalid, the screen gives visible feedback explaining that state at prototype level.
- [ ] Given the map is too dense for the default view, a prototype zoom/focus affordance exists and is usable without breaking click targets.
- [ ] Given tactical mode is open, move and attack targets are visually distinguishable, clickable, and produce visible success/invalid feedback.
- [ ] Existing connected-loop PlayMode smoke still passes.
- [ ] Before/after evidence visibly demonstrates larger/readable map, reduced overlap, unobstructed controls, selection feedback, and zoom/focus behavior.
- [ ] CI passes.

## Verification requirements

- Unit tests: Required for any nontrivial layout/zoom/focus helper logic added.
- Unity EditMode tests: Required for pure helper/domain-adjacent validation where applicable.
- Unity PlayMode tests: Required for connected-loop regression and at least one visible selection/action/zoom or focus path where feasible.
- Integration/data validation tests: Existing validators must remain passing.
- Manual Unity scene/prefab checks: Required if scene/prefab assets change.
- Screenshot/video evidence: Required before/after screenshots. Video recommended for zoom/focus and click/action feedback.
- Performance budget: N/A; avoid expensive effects or new rendering systems.
- CI evidence: Required on PR branch and post-merge main.
- Playtest evidence: Required checklist by implementer/reviewer against the observed issues.
- TDD evidence required? Yes for helper logic or input/clickability regressions; PlayMode/manual evidence for presentation-only layout changes.
- Automation deferred? No, except manual visual judgment is supplemental and must be documented.

## Ambiguity Check

Status: PASS.

Open questions:

- None blocking for a prototype pass if the user approves this packet. Exact zoom input may be chosen by implementer from the allowed forms, prioritizing the smallest reliable implementation.

Assumptions:

- Placeholder UI remains acceptable if it is readable, understandable, and usable.
- This story may change presentation scale/layout/camera/labels/colliders/feedback, but not gameplay rules.

Out of scope:

- Final UI/art/accessibility architecture and new gameplay systems.

Allowed stubs/mocks:

- Primitive prototype visuals and debug labels as listed above.

Human-approved exceptions:

- Human approval recorded on 2026-06-10: implement this exact QA-004 playability/readability packet next. Exact zoom/focus control may be chosen by the implementer from the allowed forms, prioritizing smallest reliable implementation.

## Branch / PR requirements

- Branch name: `story/STORY-QA-004-playability-map-scale-zoom-ui-clarity`
- PR title: `STORY-QA-004 Playability map scale, zoom, and UI clarity pass`
- Required linked story ID: `STORY-QA-004`
- Required linked GDD/ADR/control docs: strategic-map, tactical-combat, control-manifest, testing-strategy, CI/build automation.
- Required root/scoped AGENTS.md instructions: Unity repo root/scoped AGENTS.md.
- Required evidence summary: before/after screenshots/video, user-observed issues checklist, changed files, tests/checks, CI, remaining UX debt.
- Required omissions section: no final UI/art, no new gameplay systems, no final accessibility pass, no content/balance expansion.

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
- [x] Dependencies are listed and satisfied or marked blocking.
- [x] Acceptance criteria are observable and testable.
- [x] Verification requirements are defined according to `docs/architecture/testing-strategy.md`.
- [x] Required automated tests/validators/PlayMode evidence are listed, or approved exceptions are documented.
- [x] Ambiguity Check status is PASS.
- [x] Branch / PR / CI traceability requirements are stated.
- [x] Human approval has been given or delegated gate approval is recorded.

## DONE gate

- [x] Implementation matches approved story scope.
- [x] Acceptance criteria pass.
- [x] Required verification evidence exists.
- [ ] Required automated tests, validators, PlayMode/smoke evidence, and manual evidence pass, or human-approved exceptions are documented.
- [x] No unauthorized design or architecture decisions were introduced.
- [x] Omissions/stubs/mocks/deferred work are explicitly documented.
- [x] PR/code review is complete.
- [x] CI passes or human-approved exceptions are documented.
- [x] Required docs were updated in the correct source-of-truth layer.

## Verdict

DONE / merged. Acceptance is limited to current prototype readability/playability; final UI/art/accessibility remain deferred by story scope.
