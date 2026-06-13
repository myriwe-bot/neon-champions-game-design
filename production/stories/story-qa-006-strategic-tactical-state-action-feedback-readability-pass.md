---
title: STORY-QA-006 Strategic and Tactical State/Action Feedback Readability Pass
type: story
status: ready
phase: production
owner: shared
created: 2026-06-13
updated: 2026-06-13
source_lore: []
related:
  [
    production/epics/epic-vslice-mvp-005-champion-command-and-operations-on-ramp,
    production/stories/story-cmd-004-tactical-command-usability-and-targeting-pass,
    design/gdd/game-pillars,
    design/gdd/strategic-map,
    design/gdd/tactical-combat,
    docs/architecture/control-manifest,
    docs/architecture/testing-strategy,
    docs/architecture/ci-build-automation,
  ]
approval: approved
---

# STORY-QA-006 Strategic and Tactical State/Action Feedback Readability Pass

## Status

READY / approved for Codex implementation. Human playtest on 2026-06-13 rejected EPIC-005 closeout and approved a short QA/playability repair train. This first story is the narrow readability blocker: the player cannot reliably tell current state, clickable actions, denial reasons, or action results across strategic and tactical modes.

## Human playtest source

Preserve these complaints as implementation authority and acceptance drivers:

- Strategic turn ownership: “Not really” clear whose turn it is.
- Strategic position/state: selected Champion is visible, but with some nodes “it is unclear” where the Champion is.
- Reachability: mostly visible, but route/node meaning is only “somewhat” clear.
- Guard/site state: guarded vs unguarded is unclear; site/objective state is not meaningful enough.
- Turn changes: “I am unsure what changes each turn.”
- Tactical current actor: “No” — the active stack is not clear, and both stacks appear selectable.
- Tactical sides/targets: friendly vs enemy is “not really” clear; legal attacks are not clear; attacking feels like selecting the other army.
- Tactical results: attack/damage/result feedback is not understood.
- Champion Command: ability availability is visible, but what abilities do and why denials happen is not understood.
- UX blockers explicitly selected: clickable affordances, denial reasons, result feedback, and battle completion/attack understanding.

## Player/design value

Make the current prototype readable enough to judge the loop. This story should not add depth; it should let a player answer:

- Whose turn is it?
- Who is selected / active?
- What can I click now?
- Why was this action denied?
- What changed after the action?
- Which tactical stack is mine, which is enemy, and who acts next?

## Implementation scope

One narrow cross-mode readability pass:

### Strategic state clarity

- Make active faction, turn number, round number, selected Champion, and active Champion clear in the visible HUD/panels.
- Make selected Champion location clear enough even when nodes overlap or labels are sparse.
- Make guarded / unguarded / controlled / objective site state explicit in visible prototype text or simple markers.
- Make reachable route/node information easier to parse from the current state.
- Add or improve result text for move, invalid move, site interaction, battle result return, and end turn so the player knows what changed.

### Tactical state clarity

- Make tactical mode, current side, current active stack, and current stack owner visually/textually obvious.
- Make friendly vs enemy stacks distinct with prototype-safe text/color/markers.
- Make legal move destinations and legal attack targets unambiguous.
- Avoid making a click on an enemy stack look like selecting/owning that stack; attack affordance/result should say it is a target.
- Add or improve action feedback for move, invalid move, attack, invalid attack, pass/wait/defend, battle result, and next active stack.

### Command explanation clarity

- Keep existing Rally Order and Drone Strike mechanics unchanged.
- Add short player-facing explanation text for what each currently available/denied command does in this prototype:
  - Rally Order restores one lost unit on the current damaged Marshal stack and spends Command.
  - Drone Strike hits the displayed enemy target for one damage, spends Command, and uses the one Major Operation slot.
- Improve denial/result text only where needed to explain current behavior; do not change command rules.

## Out of scope

- No new mechanics, economy, objective rules, capture rules, retaliation rules, AI, pathfinding, or encounter rules.
- No map redesign away from the current node graph.
- No multi-turn objective capture.
- No Champion-vs-Champion encounter trigger redesign; that is reserved for `STORY-QA-007`.
- No new command effects, Command economy, cooldowns, progression, skill trees, or Operations UI.
- No new units, attack types, creature depth, final balance, final art, icons, VFX, audio, animation, portraits, or final lore copy.
- No save/load or persistence expansion.

## Acceptance criteria

- Given the strategic map is loaded, the visible UI clearly shows active faction, round/turn, selected Champion, active Champion, and selected Champion location.
- Given a guarded, unguarded, controlled, or objective site is visible, the player-facing text/markers distinguish those states without requiring implementation knowledge.
- Given the player attempts a legal or illegal strategic move/action, feedback states what happened or why it was denied, including the relevant Champion/site/node when possible.
- Given End Turn succeeds, feedback states the previous and new active faction/turn/round enough that the player can tell time advanced.
- Given tactical mode is active, current side/current stack/friendly/enemy identity are visibly distinct.
- Given tactical legal moves/attacks exist, legal move destinations and legal attack targets are visible and not confused with selection ownership.
- Given an attack succeeds, feedback states attacker, target, damage, target remaining count or defeat, and next active side/stack or battle result.
- Given an attack/move/command is denied, feedback states a concrete denial reason and does not mutate board/Command state.
- Given Rally Order or Drone Strike is visible, the UI explains what the command does in prototype terms and what it costs/targets.
- Existing tactical command mechanics and outcomes remain unchanged except for player-facing clarity.
- PlayMode smoke evidence captures before/after clarity for strategic state, tactical targeting/attack, command explanation/denial, and turn/action result feedback.
- `git diff --check`, relevant EditMode tests, relevant PlayMode smoke tests, and Unity Foundation CI exact-head pass before merge.

## Suggested implementation branch

`story/STORY-QA-006-state-action-feedback-readability`

## Suggested PR title

`STORY-QA-006 State and action feedback readability pass`

## Ambiguity check

Status: PASS.

Human-approved implementation constraints:

- This story is a readability repair, not a systems expansion.
- Preserve the user's concrete playtest complaints as acceptance drivers.
- Improve visible state, action affordances, denial reasons, and result feedback across strategic and tactical modes.
- May adjust prototype text, color, markers, buttons, result summaries, and presentation snapshots as needed.
- Must not add new mechanics, map structure, objective rules, encounter rules, final art/content, or command behavior.
- If implementation discovers that a requested clarity fix requires changing a gameplay rule, stop and report the rule-change need instead of expanding scope.

## Evidence requirements

Create or update `production/evidence/STORY-QA-006/README.md` in the Unity repo and include PNG evidence for at least:

1. Strategic initial/selected state showing active faction, turn/round, selected/active Champion, reachable/state markers.
2. Strategic action result or denial showing what changed or why it failed.
3. Tactical active stack + friendly/enemy + legal target clarity before attack.
4. Tactical attack result showing attacker, target, damage/result, and next active state or battle result.
5. Command explanation/denial/result showing Rally/Drone meaning and reason/cost/target.

README must include tests run, CI URL, omissions/deferred work, and confirmation that mechanics/rules were not expanded.
