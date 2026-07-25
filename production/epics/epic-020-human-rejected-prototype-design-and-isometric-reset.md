---
title: EPIC-020 Human-Rejected Prototype Design and Isometric Reset
type: epic
status: active
phase: production
owner: human
created: 2026-07-24
updated: 2026-07-25
approval: approved
related: [design/gdd/product-constitution, design/gdd/strategic-map, design/ux/player-shell, production/playtests/playtest-journal, production/stories/story-reset-001-readable-isometric-core-loop-replacement-slice]
---

# EPIC-020 Human-Rejected Prototype Design and Isometric Reset

## Outcome

Replace the rejected graph/dashboard first-run experience with a small, conventional, readable isometric adventure-game slice that makes the intended base-growth, Champion movement, encounter, and rival-pressure loop judgeable by an unaided human.

## Human authority

Approved directly by the owner on 2026-07-24 after stopping the playtest immediately and reporting that the game did not resemble the discussed product or its inspiration games, movement and art were unreadable, bases could not be opened, objectives and text were confusing, the shell had too many buttons, and the game was “not fun AT ALL.”

The owner then approved the proposed reset direction and requested immediate implementation where feasible.

## Product correction

- Freeze new feature breadth.
- Treat existing Domain/Application systems as reusable infrastructure, not proof of an accepted game.
- Use a normal isometric physical-map metaphor with readable preliminary art.
- Make bases persistent, recognizable, directly clickable world landmarks.
- Give bases a quiet dedicated screen with a few clearly defined buildings.
- Make the first loop obvious: open base, build/recruit, select Champion, choose visible destination, move/interact, receive a readable consequence, react to rival/objective.
- Remove dashboard density and quarantine unexplained advanced prototype systems from normal first-run play.
- Reopen final movement/topology choice after the replacement slice is human-playable; graph legality may remain temporary and hidden.

## Capability sequence

1. `STORY-RESET-001` — DONE / merged / `BLOCKED — REJECT HUMAN PLAYABILITY CLOSEOUT`: readability improved, but objective/rival/combat and meaningful decisions did not land.
2. Immediate bounded usability repair — Unity PR #191; no game-design expansion.
3. Reference research plus owner co-design of one new core-fun hypothesis — ACTIVE.
4. Movement-model decision — DRAFT; the replaytest proves the current endpoint-only graph feels spatially empty, but does not by itself approve a full tile/hex rewrite.
5. Objective/economy/building/Champion/unit/combat redesign — DRAFT and not implementation authority until the new hypothesis is approved.

## Gate

No new gameplay feature story becomes READY until the owner can launch, understand the goal, open a base, understand at least one building and recruit choice, select and move a Champion through a physical map, and describe the immediate loop without developer explanation.

## Verdict

ACTIVE / feature freeze. `STORY-RESET-001` is closed with rejected human playability verdict. PR #191 may merge only as a bounded defect repair; no broader gameplay packet is READY while the next fun hypothesis is being co-designed.
