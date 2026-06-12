---
title: STORY-LOOP-004 Objective, Champion Combat, and Casualty Stakes Smoke
type: story
status: done
phase: production
owner: shared
created: 2026-06-10
updated: 2026-06-12
source_lore: []
related:
  [
    design/gdd/strategic-map,
    design/gdd/tactical-combat,
    docs/architecture/control-manifest,
    docs/architecture/testing-strategy,
    docs/architecture/ci-build-automation,
    production/epics/epic-vslice-mvp-003-scenario-objective-champion-combat-and-casualty-stakes,
    production/stories/story-obj-001-scenario-objective-state-and-victory-feedback,
    production/stories/story-obj-002-guarded-site-defender-strength-tiers,
    production/stories/story-tac-007-simple-stack-strength-persistence,
    production/stories/story-tac-008-champion-vs-champion-tactical-encounter-path,
  ]
approval: approved
---

# Story: STORY-LOOP-004 Objective, Champion Combat, and Casualty Stakes Smoke

## Status

DONE / merged. Unity PR #32 merged on 2026-06-12 at merge commit `2ed6d38624bc7aabd824ec1ce2162e6ce7523dd2`. Post-merge `main` Unity CI passed: https://github.com/myriwe-bot/neon-champions-unity/actions/runs/27398328933.

LOOP-004 remains a pure connected-smoke/evidence story. Its evidence informs whether EPIC-VSLICE-MVP-003 is ready for human closeout/playtest acceptance or needs a narrow follow-up; the epic must not close automatically from CI alone.

## Story type

Playtest + Integration + UX/Smoke.

## Estimate

- Size: M.
- Basis: connects already-merged objective, defender tier, stack persistence, and same-node Champion-vs-Champion paths into one end-to-end smoke/evidence story. It should mostly add/adjust smoke orchestration, assertions, and evidence, not new gameplay systems.

## Parent epic

- Epic ID/path: `production/epics/epic-vslice-mvp-003-scenario-objective-champion-combat-and-casualty-stakes.md`.

## User/player/system value

As a vertical-slice tester, I need one clear smoke path proving the current objective/casualty/Champion-combat slice works together, so we can decide whether EPIC-VSLICE-MVP-003 is ready for closeout/playtest or needs a narrow usability follow-up.

## Source requirements

- `design/gdd/strategic-map.md` §§6, 8, 10, 11, 12, 13, 14 for sites, control, resources, recruitment, objective/victory hooks, Champion state, and tactical handoff.
- `design/gdd/tactical-combat.md` §§3-7 and post-battle/result sections for stack combat, battle end, casualties, and return to strategic state.
- `docs/architecture/control-manifest.md` §§1, 2, 4, 5, 6, 7, 9, 10.
- `docs/architecture/testing-strategy.md`.
- `docs/architecture/ci-build-automation.md`.
- Parent epic: `EPIC-VSLICE-MVP-003`.
- Baseline: Unity `main` after PR #31 / merge commit `1d1aa0473af6683ca4625a23eb7e0a0d240cc44d`.

## Problem statement

OBJ-001, OBJ-002, TAC-007, and TAC-008 each prove a slice of objective, defender tier, casualty persistence, or Champion-vs-Champion routing. The epic still needs a single integration smoke that demonstrates these stakes together in the current prototype and produces readable evidence for human review.

## In scope

- Add/extend a deterministic PlayMode smoke path that exercises the current vertical-slice chain:
  - objective site visibility/status;
  - guarded-site defender tier visibility;
  - tactical battle launch and result return;
  - visible stack-count/casualty persistence after battle;
  - same-node Champion-vs-Champion encounter launch/result feedback;
  - defeated Champion placeholder status where applicable;
  - objective completion/victory feedback where current mechanics support it.
- Add assertions that the player-facing HUD/text communicates what happened: objective status, defender tier, changed army stack count, Champion battle winner/loser, and defeated status.
- Produce PNG evidence under `production/evidence/STORY-LOOP-004/` showing the connected smoke path at key moments.
- Keep existing OBJ-001, OBJ-002, TAC-007, and TAC-008 tests/checks green.
- Update evidence and PR body with exact CI links, screenshots, omissions, and any accepted rough edges.

## Out of scope

- New strategic AI, pursuit, enemy autonomous initiation, or full encounter system.
- New objective archetypes, campaign progression, save/load, or full victory/loss structure beyond existing placeholder objective/victory hooks.
- Healing/recovery/casualty economy, revival, hospitals, reserves, or reinforcement logistics.
- New tactical abilities, cover, LOS, morale, ammo/status effects, or final combat balance.
- Final UI/art/accessibility, final Champion/faction/unit names, lore copy, portraits, VFX, audio, or content expansion.
- Broad layout/readability redesign unless the smoke is impossible to evidence; if so, stop and propose a narrow QA/playability follow-up instead of expanding this story.

## Allowed stubs, mocks, placeholders, or temporary data

Allowed:

- Existing placeholder Champion, faction, unit, stack, site, objective, and localization IDs.
- Deterministic smoke/test interactions rather than organic AI/player discovery.
- Existing crude tactical board and placeholder HUD/result text.
- PNG evidence from CI/local smoke capture.

Not allowed:

- Hidden mutation outside approved application/domain result paths.
- Fake screenshot/evidence that does not come from the actual Unity scene/test path.
- New mechanics added only to make the smoke pass.
- Broad UI redesign or final content work under a smoke-story label.

## Dependencies

- Required prior stories:
  - `STORY-OBJ-001` DONE / merged in Unity PR #28.
  - `STORY-OBJ-002` DONE / merged in Unity PR #29.
  - `STORY-TAC-007` DONE / merged in Unity PR #30.
  - `STORY-TAC-008` DONE / merged in Unity PR #31.
- Required architecture decisions:
  - Existing battle setup/result/application and presentation boundaries remain binding.
  - Current Unity root/scoped `AGENTS.md` rules remain binding.

## Acceptance criteria

- [ ] Given the smoke starts from the current MVP scenario, objective status and guarded defender tier are visible before battle.
- [ ] Given a guarded battle is resolved, the tactical result returns to the strategic map and visible army stack count reflects persisted casualties.
- [ ] Given a same-node Champion-vs-Champion encounter is triggered, the tactical path launches and result feedback identifies both placeholder Champions and winner/loser.
- [ ] Given a Champion is defeated in the smoke, defeated placeholder status is visible without adding recovery/victory systems beyond existing hooks.
- [ ] Given the objective path is completed, existing objective/victory feedback remains visible and correct.
- [ ] Existing OBJ-001, OBJ-002, TAC-007, and TAC-008 regression coverage remains green.
- [ ] PNG evidence shows the connected smoke path at readable key moments.
- [x] CI passes on PR branch and post-merge `main`.

## Verification requirements

- Unit/EditMode tests: required only if smoke orchestration exposes a domain/application gap; otherwise existing regressions may cover lower-level rules.
- Unity PlayMode tests: required for the connected smoke path.
- Placeholder validator: must remain passing.
- Screenshot/video evidence: PNG evidence required under `production/evidence/STORY-LOOP-004/` or equivalent story evidence path.
- CI evidence: required on PR branch and post-merge main if merged.
- TDD evidence required? Yes for any new production logic; smoke-only orchestration should still add failing PlayMode assertions before implementation.
- Automation deferred? No, except final visual/readability judgement is supplemental.

## Ambiguity Check

Status: PASS.

Human-approved decisions recorded on 2026-06-11:

1. LOOP-004 is a pure connected-smoke/evidence story. It may not broaden into gameplay, UI, AI, recovery, victory/loss, content, balance, or accessibility work.
2. Stop condition: if a real gameplay or UI blocker prevents the smoke from being exercised or evidenced, stop and report instead of expanding scope. The follow-up should be a narrow QA/playability or prerequisite story.
3. EPIC-VSLICE-MVP-003 must not close automatically from CI alone. Use LOOP-004 evidence to decide whether the epic is ready for closeout/playtest acceptance or needs a follow-up.

## Branch / PR requirements

- Branch name: `story/STORY-LOOP-004-objective-champion-combat-casualty-smoke`
- PR title: `STORY-LOOP-004 Objective, Champion combat, and casualty stakes smoke`
- Required linked story ID: `STORY-LOOP-004`
- Required evidence summary: connected smoke path, visible objective/tier/casualty/Champion-result evidence, test commands, CI, screenshots, omissions.
- Required omissions section: no strategic AI, no full encounter system, no healing/recovery/casualty economy, no final content/balance/lore, no broad UI redesign, no final accessibility/art.

PR must explicitly list known omissions, stubs, mocks, assumptions, deferred work, or state `No known omissions`.

## Story readiness gate

- [x] Story has stable ID, title, type, status, and parent epic.
- [x] User/player/system value is clear.
- [x] Exact GDD source sections are linked.
- [x] Exact ADR/architecture/control-manifest sources are linked.
- [x] Relevant root/scoped AGENTS.md instructions are identified.
- [x] In-scope work is concrete and bounded.
- [x] Out-of-scope work is explicit.
- [x] Stubs/mocks/placeholders are explicitly listed.
- [x] Dependencies are listed and satisfied.
- [x] Acceptance criteria are observable and testable.
- [x] Verification requirements are defined.
- [x] Ambiguity Check status is PASS.
- [x] Human approval has been given for implementation / READY promotion.

## DONE gate

- [x] Implementation matches approved story scope.
- [x] Acceptance criteria pass.
- [x] Required verification evidence exists.
- [x] Required automated tests, validators, PlayMode/smoke evidence, and manual evidence pass.
- [x] No unauthorized design or architecture decisions were introduced.
- [x] Omissions/stubs/mocks/deferred work are explicitly documented.
- [x] PR/code review is complete.
- [x] CI passes on PR branch and post-merge `main`.
- [x] Required docs were updated in the correct source-of-truth layer.

## Merge evidence

- Unity PR: #32 — https://github.com/myriwe-bot/neon-champions-unity/pull/32
- Merge commit: `2ed6d38624bc7aabd824ec1ce2162e6ce7523dd2`
- Post-merge main CI: passed — https://github.com/myriwe-bot/neon-champions-unity/actions/runs/27398328933
- Evidence package: `production/evidence/STORY-LOOP-004/README.md` in the Unity repo.

## Verdict

DONE / merged. STORY-LOOP-004 is closed; EPIC-VSLICE-MVP-003 now needs human closeout/playtest review before being marked DONE or before any follow-up story is approved.
