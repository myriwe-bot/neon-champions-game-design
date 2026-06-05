---
title: STORY-TAC-005 Basic Tactical Player Controls
type: story
status: implemented
phase: production
owner: shared
created: 2026-06-04
updated: 2026-06-04
source_lore: []
related:
  [
    design/gdd/tactical-combat,
    docs/architecture/control-manifest,
    docs/architecture/testing-strategy,
    docs/architecture/ci-build-automation,
    production/epics/epic-vslice-mvp-002-larger-map-bases-recruitment-minimal-tactical-combat,
    production/stories/story-loop-002-visible-guarded-site-capture-smoke,
  ]
approval: approved
---

# Story: STORY-TAC-005 Basic Tactical Player Controls

## Status

DONE / merged. Implemented in Unity PR #20 and squash-merged on 2026-06-05 as `4bd753cfbb861a49f96daf90378a674d27be5d4f`; branch `story/STORY-TAC-005-basic-tactical-player-controls` was deleted. Final PR-head CI passed on head `6824bacd1a239bf2c82b4dbfec1f96a5b8cfa797`; post-merge Unity main verification passed on merge commit `4bd753cfbb861a49f96daf90378a674d27be5d4f` via workflow dispatch run https://github.com/myriwe-bot/neon-champions-unity/actions/runs/27016431640.

## Story type

Tactical UI/Input + Integration + UX/Smoke.

## Estimate

- Size: M.
- Basis: existing tactical domain already has tiny hex board, stack placement, movement/attack resolution, battle end, and result return. This story wires minimal player-facing controls without adding full tactical depth.

## Parent epic

- Epic ID/path: `production/epics/epic-vslice-mvp-002-larger-map-bases-recruitment-minimal-tactical-combat.md`.

## User/player/system value

As a player/designer, I want the tactical board to accept basic commands instead of being a one-button auto-resolve view, so that future tactical playtests can judge movement, attack, pass/wait, and result return as player actions.

## Source requirements

- `design/gdd/tactical-combat.md` §3 Design Principles.
- `design/gdd/tactical-combat.md` §4 MVP Scope, especially movement, melee/ranged attack, defend/brace, wait, and objective interaction as MVP action families.
- `design/gdd/tactical-combat.md` §5 Core Combat Loop, steps 5-10.
- `design/gdd/tactical-combat.md` §6.0 Grid Decision.
- `design/gdd/tactical-combat.md` §6.3 AP and Actions.
- `design/gdd/tactical-combat.md` §6.10 Post-Battle Resolution.
- `docs/architecture/control-manifest.md` §§1, 2, 4, 5, 6, 7, 9, 10.
- `docs/architecture/testing-strategy.md`.
- `docs/architecture/ci-build-automation.md`.

## In scope

- Tactical-board player controls for the existing minimal guarded-site battle path:
  - visible acting stack / acting side;
  - select or clearly indicate legal movement destination(s);
  - move the acting stack to a legal empty hex;
  - attack a legal enemy target;
  - pass/wait/defend as a minimal explicit fallback action that ends the current activation without damage.
- A deterministic tiny activation order sufficient for the current two-side MVP battle: after an acting stack uses move+attack or pass/wait/defend, control advances to the next undefeated opposing stack or resolves the battle if an end condition is reached.
- Preserve the existing strategic-to-tactical-to-strategic result path: a player-driven tactical win still returns a real `BattleResult` and applies site control on the strategic map.
- Clear HUD copy explaining that this is minimal tactical control, not final tactical combat.
- EditMode tests for new command/activation behavior and PlayMode smoke for at least one player-driven tactical capture path.
- Evidence package with controls checklist, screenshot/video if available, CI, and omissions.

## Out of scope

- Full AP economy, initiative model, abilities, morale, cover, LOS, objective interactions beyond current capture smoke, ranged-vs-melee balance, unit roster balance, animations, final UI/art/audio, hotkeys, accessibility pass, strategic AI, larger map, bases, or recruitment.
- Adding final tactical data schemas or content.
- Replacing approved domain architecture with a new tactical engine.

## Allowed stubs, mocks, placeholders, or temporary data

Allowed:

- Placeholder button labels, target markers, legal-move highlights, and debug/HUD strings.
- Minimal pass/wait/defend semantics as an explicit no-damage activation-ending action.
- Current tiny board and placeholder attacker/guard stacks.

Not allowed:

- Hiding player control behind a one-button auto-resolve.
- Adding full tactical mechanics not authorized above.
- Inventing final faction/unit names, art, balance, or content.

## Acceptance criteria

- [ ] Given the tactical view is entered from the guarded-site smoke, the UI visibly identifies the acting side/stack and available basic actions.
- [ ] Given the acting stack has a legal empty adjacent hex, the player can command a movement and see the stack marker update without corrupting occupancy.
- [ ] Given a legal enemy target is in range after movement or from the current position, the player can command an attack and see damage/defeat reflected.
- [ ] Given the player chooses pass/wait/defend, the current activation ends without damage and control advances according to the minimal deterministic activation order.
- [ ] Given the guard is defeated by player-driven actions, a real `BattleResult` returns to strategy and the guarded site becomes controlled by the attacking faction.
- [ ] Given illegal movement or attack input, the command is rejected with visible feedback and no state mutation beyond the feedback.
- [ ] CI passes.

## Verification requirements

- Unity EditMode tests: Required for tactical command validation, occupancy/no-mutation rejection, pass/wait/defend activation advancement, and battle-result return after player-driven win.
- Unity PlayMode tests: Required for the visible guarded-site tactical-control smoke if feasible; otherwise document a blocker and include manual screenshot/video evidence as a temporary exception.
- Manual Unity scene/prefab checks: Required if presentation/input wiring changes.
- Screenshot/video evidence: Required for tactical controls and result return.
- CI evidence: Required.
- TDD evidence required? Yes for new command/activation logic and bug fixes.

## Ambiguity Check

Status: PASS.

Resolved by human direction on 2026-06-04:

- Tactical view currently being one-button/unusable is a real follow-up problem.
- This is not a full tactics redesign; it is a minimal player-control step before deeper tactical systems.

Assumptions:

- `Pass`, `Wait`, and `Defend/Brace` may share temporary activation-ending semantics for this story, but the UI/evidence must label the limitation clearly.
- Legal movement and attack should reuse existing minimal tactical domain behavior where possible.

## Branch / PR requirements

- Branch name: `story/STORY-TAC-005-basic-tactical-player-controls`
- PR title: `STORY-TAC-005 Basic tactical player controls`
- Required linked story ID: `STORY-TAC-005`
- Required evidence summary: controls checklist, tests, screenshot/video if available, CI, omissions/stubs.

PR must explicitly list known omissions, stubs, mocks, assumptions, deferred work, or state `No known omissions`.

## Verdict

DONE. Implementation matched the minimal player-control layer needed to make the existing tactical board usable for movement, attack, pass/wait/defend, and result return. Remaining tactical depth is deferred to later approved stories.
