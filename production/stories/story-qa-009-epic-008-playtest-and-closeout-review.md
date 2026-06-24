---
title: STORY-QA-009 EPIC-008 Playtest and Closeout Review
type: story
status: done
phase: production
owner: shared
created: 2026-06-19
updated: 2026-06-19
source_lore: [greenland, qxz-meridian, white-sky]
related:
  [
    production/epics/epic-vslice-mvp-008-faction-armies-recruitment-and-tactical-role-identity,
    production/planning/epic-008-faction-armies-recruitment-and-role-identity-plan,
    production/stories/story-army-001-mvp-faction-unit-definitions-and-roster-seed,
    production/stories/story-army-002-tactical-role-behaviors-and-sensor-lock,
    production/stories/story-army-003-fixed-recruitment-offers-and-army-summary,
    production/stories/story-army-004-composition-consequence-scenario,
    design/gdd/strategic-map,
    design/gdd/tactical-combat,
    design/gdd/faction-unit-rosters,
    docs/architecture/control-manifest,
    docs/architecture/testing-strategy,
    docs/architecture/ci-build-automation,
  ]
approval: approved
---

# STORY-QA-009 EPIC-008 Playtest and Closeout Review

## Status

DONE / merged. Unity PR #70 merged as `7d605dcc0a00f12bd8b67d389f176a700b2baf5e`; post-merge Unity Foundation CI passed: https://github.com/myriwe-bot/neon-champions-unity/actions/runs/28123164904. Closeout verdict recommends `CLOSE EPIC`; human next-direction acceptance is still required before promoting any next implementation story to READY.

## Story type

QA + Playability Review + Epic Closeout Decision.

## Parent epic

- [EPIC-VSLICE-MVP-008 Faction Armies, Recruitment, and Tactical Role Identity](../epics/epic-vslice-mvp-008-faction-armies-recruitment-and-tactical-role-identity.md)

## User/player/system value

As a player and designer, I want a compact end-to-end review of EPIC-008’s army/recruitment identity slice so we can decide whether faction armies now create enough strategic/tactical meaning to close the epic, repair one blocker, or choose the next deeper system.

## Source requirements

Exact source references:

- `production/stories/story-army-001-mvp-faction-unit-definitions-and-roster-seed.md` for MVP roster and unit definition proof.
- `production/stories/story-army-002-tactical-role-behaviors-and-sensor-lock.md` for tactical role/Sensor Lock proof.
- `production/stories/story-army-003-fixed-recruitment-offers-and-army-summary.md` for recruitment, offer consumption, army summary, and tactical handoff proof.
- `production/stories/story-army-004-composition-consequence-scenario.md` for composition consequence proof.
- `production/epics/epic-vslice-mvp-008-faction-armies-recruitment-and-tactical-role-identity.md` for epic capability goal and DONE gate.
- `production/planning/epic-008-faction-armies-recruitment-and-role-identity-plan.md` Slice E.
- `design/gdd/strategic-map.md` §§2-8 and §§10-13 for recruit/fight/return loop.
- `design/gdd/tactical-combat.md` §§3-6.7 for stack combat and readable tactical identities.
- `design/gdd/faction-unit-rosters.md` for faction army identity goals and naming guardrails.
- `docs/architecture/control-manifest.md` §§1, 2, 4, 5, 6, 7, 9, 10.
- `docs/architecture/testing-strategy.md`.
- `docs/architecture/ci-build-automation.md`.

## In scope

Concrete closeout target:

- Run a focused EPIC-008 playtest/review path: recruit -> inspect army -> fight -> suffer losses -> return to strategic map -> judge changed composition.
- Use existing implemented evidence where possible rather than inventing a new mechanic.
- Add or update a story-scoped closeout evidence README under `production/evidence/STORY-QA-009/` summarizing what EPIC-008 now proves and what remains deferred.
- Add a small automated smoke/verification layer only if needed to make the closeout repeatable; prefer reusing existing ARMY-001..004 tests/evidence when sufficient.
- Record a clear closeout verdict: `CLOSE EPIC`, `ONE NARROW FOLLOW-UP`, or `REJECT CLOSEOUT`.
- If closing or recommending next direction, list 2-4 next-epic options with a recommended default, but do not promote any next epic/story to READY.

## Out of scope

Not authorized by this story:

- No new unit definitions, tactical role behavior, recruitment economy, town/economy system, upgrades, strategic AI, final art/audio/VFX, or scenario editor.
- No broad balance pass or mirrored QXZ implementation unless the human approval explicitly changes this story scope before READY.
- No new next-epic implementation packet.
- No hard-canon rename of Home Rule Coalition.

## Allowed stubs, mocks, placeholders, or temporary data

- Closeout may reference existing prototype UI/evidence and documented omissions instead of creating new gameplay content.
- If one blocker is found, document it as a proposed follow-up rather than fixing it inside this closeout unless the fix is tiny, test-covered, and explicitly still QA/closeout scoped.
- Decision-brief text may be committed as production review material, but it must not authorize new runtime work without later human approval.

## Dependencies

- `STORY-ARMY-001` DONE / merged.
- `STORY-ARMY-002` DONE / merged.
- `STORY-ARMY-003` DONE / merged.
- `STORY-ARMY-004` DONE / merged.
- Existing Unity Foundation CI and checked-in EPIC-008 evidence packages.

## Acceptance criteria

- [ ] Closeout review walks the recruit -> inspect army -> fight -> loss/result -> return loop using current implementation/evidence.
- [ ] Review explicitly judges whether EPIC-008 met its player-facing capability goal: faction units + recruitment + tactical role identity + composition consequence.
- [ ] Review separates completed proof points, deferred scope, and true blockers.
- [ ] Review records one of: `CLOSE EPIC`, `ONE NARROW FOLLOW-UP`, or `REJECT CLOSEOUT`.
- [ ] If no true blocker remains, review recommends closing EPIC-008 and proposes next-epic direction options without promoting one to READY.
- [ ] If a true blocker remains, review defines exactly one narrow follow-up candidate and keeps all broader next directions pending.
- [ ] Evidence documents tests/evidence reviewed, screenshots or evidence paths, CI, omissions/deferred work, and next-direction recommendation.

## Verification requirements

- Unit/EditMode tests: only required if new closeout code or regression checks are added.
- PlayMode/smoke tests: required if new closeout evidence is captured; otherwise cite current passing EPIC-008 story CI/evidence.
- Screenshot/video evidence: use existing ARMY-001..004 evidence and add closeout summary under `production/evidence/STORY-QA-009/` if approved.
- CI evidence: Unity Foundation CI exact-head before merge if any Unity repo changes are made.
- TDD evidence required? N/A unless new code is added.

## Ambiguity Check

Status: PASS.

Human-approved answers recorded 2026-06-24:

1. STORY-QA-009 is closeout-first. It may include only tiny test/evidence polish if needed to make the closeout repeatable; no new gameplay mechanics or broad repair work.
2. Codex may recommend exactly one of `CLOSE EPIC`, `ONE NARROW FOLLOW-UP`, or `REJECT CLOSEOUT`. The recommendation is not itself approval to close the epic or begin another implementation story.
3. Include 2-4 next-epic options and a recommended default as decision options only; do not promote any next epic/story to READY.

Human-approved exceptions:

- Tiny QA/evidence/test polish is allowed only if it remains story-scoped and does not add new gameplay.

## Branch / PR requirements

- Branch name after approval: `story/STORY-QA-009-epic-008-playtest-closeout-review`
- PR title after approval: `STORY-QA-009 EPIC-008 playtest and closeout review`
- Required linked story ID: `STORY-QA-009`.
- Required evidence summary: tests/evidence reviewed, any new evidence path, CI run URL if Unity changes are made.
- Required omissions section: explicitly list known omissions/stubs/placeholders/deferred work or state `No known omissions`.

## Story readiness gate

- [x] Story has stable ID, title, type, status, and parent epic.
- [x] User/player/system value is clear.
- [x] Exact GDD source section is linked or explicitly N/A.
- [x] Exact ADR/architecture/control-manifest source is linked or explicitly N/A.
- [x] Relevant root/scoped AGENTS.md instructions are identified.
- [x] In-scope work is concrete and bounded.
- [x] Out-of-scope work is explicit.
- [x] Stubs/mocks/placeholders are explicitly listed.
- [x] Dependencies are listed and satisfied.
- [x] Acceptance criteria are observable and testable.
- [x] Verification requirements are defined according to `docs/architecture/testing-strategy.md`.
- [x] Required automated tests/validators/PlayMode evidence are listed.
- [x] Ambiguity Check status is PASS.
- [x] Human approval recorded.

## DONE gate

- [x] Implementation matches approved story scope.
- [x] Acceptance criteria pass.
- [x] Required verification evidence exists: Unity `production/evidence/STORY-QA-009/README.md`.
- [x] Required automated tests, validators, and PlayMode/smoke evidence pass, or human-approved exceptions are documented.
- [x] No unauthorized design or architecture decisions were introduced.
- [x] Omissions/stubs/mocks/deferred work are explicitly documented.
- [x] PR/code review is complete.
- [x] CI passes or human-approved exceptions are documented.
- [x] Required docs were updated in the correct source-of-truth layer.

## Verdict

DONE / merged. STORY-QA-009 closeout evidence recommends `CLOSE EPIC`, with next-epic options retained as human decision options only.
