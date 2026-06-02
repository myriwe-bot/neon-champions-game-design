---
title: Strategic MVP Story Train 001
type: milestone
status: in-review
phase: production
owner: shared
created: 2026-06-02
updated: 2026-06-02
source_lore: []
related: [production/epics/epic-strat-mvp-001-strategic-mvp-core-loop, production/stories/story-strat-001-scenario-map-graph-state, production/stories/story-strat-002-hotseat-turn-ownership, production/stories/story-strat-003-champion-route-movement, production/stories/story-strat-vis-001-minimal-strategic-map-presentation, production/stories/story-strat-input-001-select-champion-and-route-move, production/stories/story-strat-ui-001-minimal-hotseat-hud, production/stories/story-loop-001-minimal-local-hotseat-strategic-loop-smoke, production/stories/story-tac-001-battle-setup-result-dto-contracts]
approval: pending
---

# Strategic MVP Story Train 001

## Purpose

Define the first safe Codex implementation train after STORY-STRAT-001, with an explicit bias toward making the strategic loop visible and player-testable as early as possible.

The goal is to increase Codex utilization without giving it a broad, drift-prone mandate. Codex should implement one READY story at a time, on one branch/PR at a time, with CI and review before continuing. Crude visual/input/HUD stories are intentionally inserted before deeper site/battle work so humans can test the local-hotseat movement/end-turn loop early.

## Sequence

| Order | Story | Status | Why now | Stop before next if |
|---:|---|---|---|---|
| 0 | [[production/stories/story-strat-001-scenario-map-graph-state|STORY-STRAT-001 Scenario Map Graph State]] | Implemented/reviewed in Unity branch; design story remains approved | Foundation state/validation already exists | PR not merged or CI/review regresses |
| 1 | [[production/stories/story-strat-002-hotseat-turn-ownership|STORY-STRAT-002 Hotseat Turn Ownership]] | READY-candidate | Turns give all later actions an owner and cadence | CI fails, turn rules require UX/design invention, or scope leaks into income/site behavior |
| 2 | [[production/stories/story-strat-003-champion-route-movement|STORY-STRAT-003 Champion Route Movement]] | READY-candidate | Movement makes the graph playable while staying pure domain | CI fails, pathfinding/modifiers/UI are needed, or turn ownership is unresolved |
| 3 | [[production/stories/story-strat-vis-001-minimal-strategic-map-presentation|STORY-STRAT-VIS-001 Minimal Strategic Map Presentation]] | READY-candidate | Make the map visible early with crude nodes/routes/Champion markers before deeper invisible systems accumulate | CI fails, scene/prefab wiring is unsafe, presentation needs architecture/package changes, or visuals imply final art/content |
| 4 | [[production/stories/story-strat-input-001-select-champion-and-route-move|STORY-STRAT-INPUT-001 Select Champion and Route Move]] | READY-candidate | Wire the first direct player action: select active Champion and move one adjacent route | CI fails, input requires package/settings changes, invalid moves bypass domain services, or scope leaks into site interaction |
| 5 | [[production/stories/story-strat-ui-001-minimal-hotseat-hud|STORY-STRAT-UI-001 Minimal Hotseat HUD]] | READY-candidate | Make hotseat turns understandable and add End Turn so a human can play without developer guidance | CI fails, UI requires final UI architecture/art/localization decisions, or End Turn bypasses domain rules |
| 6 | [[production/stories/story-loop-001-minimal-local-hotseat-strategic-loop-smoke|STORY-LOOP-001 Minimal Local Hotseat Strategic Loop Smoke]] | READY-candidate | Confirm the crude two-faction movement/end-turn loop is actually player-testable in Unity | Smoke cannot be completed, domain/visual/HUD state disagree, or manual/PlayMode evidence is missing |
| 7 | [[production/stories/story-tac-001-battle-setup-result-dto-contracts|STORY-TAC-001 Battle Setup Result DTO Contracts]] | READY-candidate | DTO boundary unblocks guarded-site and result-application stories after the first visible loop is testable | CI fails or tactical internals are required beyond DTO shape |

## Codex execution contract

Codex may only run this train if the next story is marked READY/approved.

For each story:

1. Start from updated `main` after the previous PR merges.
2. Create the exact story branch named in the story file.
3. Read the READY story, linked GDD sections, linked architecture/control docs, Unity repo `AGENTS.md`, and scoped `AGENTS.md` files.
4. Stop if any source is draft/pending/contradictory or if the Unity working tree has unrelated changes.
5. Use TDD for production domain logic.
6. Keep scope to the story. No UI/scene/prefab/package/settings/content changes unless the story explicitly allows them.
7. Commit, push, open PR, and include evidence plus omissions section.
8. Wait for CI and review before starting the next story.

## Initial Codex prompt shape

Use a short prompt that points Codex to checked-in docs rather than pasting huge markdown:

```text
Implement the next READY story only: <STORY-ID>.
Read the story file in neon-champions-game-design, all linked GDD/ADR/control sources, and the Unity repo AGENTS.md/scoped AGENTS.md files before coding.
Work on the exact branch named in the story.
Use TDD and keep changes story-scoped.
Open a PR with evidence and omissions.
Stop on ambiguity, draft/pending sources, unrelated dirty files, failed CI, or scope expansion.
```

## Gate status

READY-candidate train. Human approval is required before marking the new stories READY and assigning Codex.
