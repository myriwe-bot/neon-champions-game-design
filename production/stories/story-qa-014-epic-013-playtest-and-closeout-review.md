---
title: STORY-QA-014 EPIC-013 Playtest and Closeout Review
type: story
status: ready
phase: production
owner: shared
created: 2026-07-02
updated: 2026-07-02
source_lore: []
related:
  [
    production/epics/epic-vslice-mvp-013-scenario-pressure-and-victory-readability,
    production/stories/story-pressure-001-objective-pressure-and-victory-readability-smoke,
    production/stories/story-pressure-002-opponent-contest-and-loss-pressure-smoke,
    design/gdd/strategic-map,
    design/gdd/tactical-combat,
    docs/architecture/control-manifest,
    docs/architecture/testing-strategy,
    docs/architecture/ci-build-automation,
  ]
approval: approved
---

# STORY-QA-014 EPIC-013 Playtest and Closeout Review

## Status

READY / approved. Human approval recorded 2026-07-02: "Approved". This is the current approved Unity implementation packet after `STORY-PRESSURE-002` merged. Unity README pointer PR #132 merged as `7d8c9739432512181b3afe3683c0fb197468b115`; exact-head pointer PR CI passed at https://github.com/myriwe-bot/neon-champions-unity/actions/runs/28580428245 and post-merge pointer main CI passed at https://github.com/myriwe-bot/neon-champions-unity/actions/runs/28580953928.

## Story type

QA / Playability Review + Narrow Fix Pass.

## Parent epic

- [EPIC-VSLICE-MVP-013 Scenario Pressure and Victory Readability](../epics/epic-vslice-mvp-013-scenario-pressure-and-victory-readability.md)

## User/player/system value

As project director, I need the merged EPIC-013 pressure/readability surface reviewed as one playable loop before closing the epic or starting a new capability train.

## Source requirements

- Parent epic: `production/epics/epic-vslice-mvp-013-scenario-pressure-and-victory-readability.md`.
- Merged Unity evidence:
  - `production/evidence/STORY-PRESSURE-001/`
  - `production/evidence/STORY-PRESSURE-002/`
- GDD/control:
  - `design/gdd/strategic-map.md` §§6, 8, 10-14.
  - `design/gdd/tactical-combat.md` current tactical handoff/result boundaries.
  - `docs/architecture/control-manifest.md`.
  - `docs/architecture/testing-strategy.md`.
  - `docs/architecture/ci-build-automation.md`.

## In scope

If approved, this story may:

- Review/run current Unity `main` at 1280x720 against the complete EPIC-013 pressure/readability surface.
- Inspect the complete pressure chain together:
  - player-side objective pressure before contest;
  - action/victory direction;
  - opponent contest/loss-pressure direction;
  - after-contest/reversed/reset/still-holder messaging;
  - at least one surrounding normal strategic interaction after pressure messaging.
- Fix only concrete player-facing readability/clickability/evidence regressions directly tied to EPIC-013 commitments, such as misleading pressure text, missing loss-direction text, unreadable HUD placement, stale evidence wording, or a broken surrounding-loop smoke.
- Add or update PlayMode smoke tests and PNG/text evidence under Unity `production/evidence/STORY-QA-014/` if a fix is made or if closeout review needs new evidence.
- Produce a concise closeout verdict recommending one of:
  - `CLOSE EPIC-013`;
  - `ONE NARROW FOLLOW-UP`;
  - `REJECT CLOSEOUT / NEEDS HUMAN PLAYTEST`.

## Out of scope

Not authorized by this story:

- No strategic AI, autonomous opponent planning, campaign scheduling, scenario generation, save/load, meta-progression, diplomacy, PR/legitimacy, or economy systems.
- No new tactical combat mechanics, unit abilities, AP, terrain, balance, battle-result semantics, or tactical AI.
- No new Intel/dirty-information mechanics, fog-of-war, false leads, counter-intel, or social graph.
- No new map topology, nodes, routes, sites, objectives, factions, resources, facilities, recruitment offers, final content/lore names, art/audio/VFX/icons, localization framework, or accessibility framework.
- No next-epic implementation story promotion without separate human approval.

## Acceptance criteria

- [ ] The merged EPIC-013 pressure/readability surface is reviewed on current Unity `main` at 1280x720.
- [ ] The review explicitly addresses player objective pressure, action/victory direction, opponent contest/loss-pressure direction, after-contest messaging, and surrounding-loop usability.
- [ ] Any concrete in-scope closeout blockers are fixed narrowly, or the story records why no fix was needed.
- [ ] Evidence under Unity `production/evidence/STORY-QA-014/` documents the inspected surface if the story is approved and run.
- [ ] Exact-head Unity Foundation CI passes before merge if any Unity PR is opened.
- [ ] Closeout verdict is recorded: `CLOSE EPIC-013`, `ONE NARROW FOLLOW-UP`, or `REJECT CLOSEOUT / NEEDS HUMAN PLAYTEST`.

## Verification requirements

- `git diff --check`.
- Placeholder validator remains green.
- EditMode tests pass if any application/domain/projection changes are made.
- PlayMode tests pass if any Unity code/UI/evidence changes are made.
- Standalone Windows64 build passes if a Unity PR is opened and the workflow runs it.
- Exact-head Unity Foundation CI before merge and post-merge main CI after merge if implemented as a Unity branch.
- If no code changes are needed, closeout documentation must still record what was inspected and why no fix was needed.

## Ambiguity Check

Status: PASS. Implementation authority granted for a narrow EPIC-013 playtest/closeout review only.

Human-approved answers / assumptions:

- Approved 2026-07-02 via user instruction: "Approved".
- Run this QA/playtest closeout packet as the next Unity step.
- Allow only narrow readability/clickability/evidence fixes directly tied to EPIC-013 commitments.
- Record a closeout verdict; do not close EPIC-013 or start a next-epic implementation story without separate human direction.

## Branch / PR requirements

- Branch name: `story/STORY-QA-014-epic-013-playtest-closeout-review`.
- PR title: `STORY-QA-014 EPIC-013 playtest and closeout review`.
- Required linked story ID: `STORY-QA-014`.
- Required evidence path: `production/evidence/STORY-QA-014/` in Unity if approved/run.
- Required verdict section: close epic, one narrow follow-up, or reject closeout / needs human playtest.

## Story readiness gate

- [x] Story has stable ID, title, type, status, and parent epic.
- [x] User/player/system value is clear.
- [x] Source requirements are linked.
- [x] In-scope work is bounded.
- [x] Out-of-scope work is explicit.
- [x] Dependencies are listed and satisfied.
- [x] Acceptance criteria are observable.
- [x] Verification requirements are defined.
- [x] Branch / PR / CI traceability requirements are stated.
- [x] Human approval has been recorded.

## Verdict

READY for implementation. Implement only this narrow EPIC-013 playtest/closeout review; broader campaign, AI, economy, tactical, dirty-information, map/content, and next-epic systems remain deferred.
