---
title: STORY-PRESSURE-002 Opponent Contest and Loss Pressure Smoke
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
    design/gdd/strategic-map,
    design/gdd/tactical-combat,
    docs/architecture/control-manifest,
    docs/architecture/testing-strategy,
    docs/architecture/ci-build-automation,
  ]
approval: approved
---

# STORY-PRESSURE-002 Opponent Contest and Loss Pressure Smoke

## Status

READY / approved. Human approval recorded 2026-07-02: "Approved". This is the current approved implementation packet after `STORY-PRESSURE-001` merged. Unity current-task pointer PR #129 merged as `764d8e9d1ca6e7fafb6e6fb9f1119a6ba08ca424`; exact-head pointer PR CI passed at https://github.com/myriwe-bot/neon-champions-unity/actions/runs/28570996363 after rerunning a transient Compile job failure, and post-merge pointer main CI passed at https://github.com/myriwe-bot/neon-champions-unity/actions/runs/28571390526. Unity current-task pointer cleanup PR #128 merged as `0ae348848268e61946344d31cbffcea63221a2f4`; exact-head pointer PR CI passed at https://github.com/myriwe-bot/neon-champions-unity/actions/runs/28567972315 and post-merge pointer main CI passed at https://github.com/myriwe-bot/neon-champions-unity/actions/runs/28568289898.

## Story type

Strategic UX + connected PlayMode smoke / pressure readability pass.

## Parent / context

Parent: `EPIC-VSLICE-MVP-013 Scenario Pressure and Victory Readability`.

`STORY-PRESSURE-001` made the player-side objective pressure/action/victory direction visible. The next narrow gap is whether the prototype can show the opponent contest/loss-pressure side of the same loop without adding strategic AI, new campaign rules, economy, or tactical mechanics.

## Player/design value

As a tester, I need to see when the opponent can contest or reverse my objective pressure, and whether that creates readable loss/threat direction, so the pressure loop feels like a contested scenario rather than a one-sided checklist.

## Source authority

Required sources:

- `production/stories/story-pressure-001-objective-pressure-and-victory-readability-smoke.md` and Unity PR #127 evidence.
- `production/epics/epic-vslice-mvp-013-scenario-pressure-and-victory-readability.md`.
- Existing objective/victory and strategic hotseat/turn ownership stories.
- `design/gdd/strategic-map.md` §§6, 8, 10-14.
- `design/gdd/tactical-combat.md` existing tactical handoff/result boundaries.
- `docs/architecture/control-manifest.md`, `docs/architecture/testing-strategy.md`, `docs/architecture/ci-build-automation.md`.

## In scope

- One connected hotseat/manual-opponent smoke over existing mechanics:
  1. start from or create a state where the player holds objective pressure;
  2. show opponent contest/loss-pressure direction using runtime state;
  3. execute the existing contest path if already supported, or document the exact supported blocker without inventing AI/campaign systems;
  4. show player-facing after-state text for contested, reset, reversed, or still-holder pressure;
  5. prove one normal strategic interaction remains usable after contest/loss-pressure messaging.
- Minimal HUD/status/evidence-label copy needed to distinguish player victory direction from opponent contest/loss direction.
- Focused EditMode/PlayMode tests for state-backed contest/loss-pressure readability.
- PlayMode/generated PNG or text evidence under Unity `production/evidence/STORY-PRESSURE-002/`.
- A concise omissions/deferred-work note naming any remaining pressure-loop gaps for human playtest.

## Out of scope

- Strategic AI/autonomous enemy planning, campaign scheduling, scenario generation, save/load, or meta-progression.
- New economy/base/recruitment mechanics.
- New tactical combat mechanics, unit abilities, AP rules, terrain rules, balance, or battle-result semantics.
- New Intel/dirty-information mechanics, fog-of-war, false leads, PR/hearts-and-minds, counter-intel, or social graph.
- New map topology, final content/lore names, art/audio/VFX/icons/localization/accessibility framework.

## Acceptance criteria

- [ ] Connected evidence shows the player-side objective pressure state before opponent contest/loss-pressure changes it.
- [ ] Connected evidence shows the opponent contest/loss-pressure path using existing mechanics or clearly records the exact currently unsupported blocker.
- [ ] After-state player-facing text clearly distinguishes contested/reset/reversed/still-holder pressure and victory/loss direction.
- [ ] The contest/loss-pressure messaging is backed by runtime/application state or existing result objects, not screenshot-only copy.
- [ ] At least one normal strategic interaction remains visibly usable after the contest/loss-pressure messaging exists.
- [ ] Existing `STORY-PRESSURE-001` objective pressure tests/evidence expectations continue to pass or are updated with equivalent stronger coverage.
- [ ] Evidence under Unity `production/evidence/STORY-PRESSURE-002/` includes before-contest, contest-action-or-blocker, after-contest/loss-direction, surrounding-loop-unbroken, and omissions/deferred-work notes.
- [ ] Exact-head Unity Foundation CI passes before merge.

## Verification requirements

Required unless a blocker is documented in PR evidence:

- `git diff --check`.
- Focused EditMode/domain/application tests for changed contest/loss-pressure status copy or result-state behavior.
- PlayMode smoke or generated PNG/text evidence for before-contest, contest-action-or-blocker, after-contest/loss-direction, and surrounding-loop-unbroken states.
- Placeholder validator.
- Standalone Windows64 build if the Unity CI workflow runs it.
- Exact-head Unity Foundation CI before merge and post-merge main CI after merge.

## Ambiguity Check

Status: PASS. Human approval recorded 2026-07-02.

Implementation defaults:

- Keep this as a narrow readability/connected-smoke story, not an AI/campaign story.
- If opponent contest is not currently executable with existing mechanics, Codex should produce state-backed blocker evidence and the narrowest follow-up recommendation rather than faking the path.

## Branch / PR requirements

- Branch name: `story/STORY-PRESSURE-002-opponent-contest-loss-pressure`.
- PR title: `STORY-PRESSURE-002 opponent contest and loss pressure smoke`.
- Required linked story ID: `STORY-PRESSURE-002`.
- Required evidence path: `production/evidence/STORY-PRESSURE-002/` in Unity.
- Required omissions section: explicitly list deferred AI/campaign/economy/tactical/dirty-information systems or state `No known omissions`.

## Story readiness gate

- [x] Story has stable ID, title, type, status, and parent/context.
- [x] User/player/system value is clear.
- [x] Source authority is explicit.
- [x] In-scope and out-of-scope are bounded.
- [x] Acceptance criteria are observable.
- [x] Verification requirements are defined.
- [x] Branch / PR / CI traceability requirements are stated.
- [x] Human implementation approval has been recorded.

## Verdict

READY for implementation. Implement only this narrow opponent-contest/loss-pressure smoke; broader AI/campaign/economy/tactical/dirty-information systems remain deferred.
