---
title: Strategic MVP Story Train 001
type: milestone
status: approved
phase: production
owner: shared
created: 2026-06-02
updated: 2026-06-03
source_lore: []
related:
  [
    production/epics/epic-strat-mvp-001-strategic-mvp-core-loop,
    production/stories/story-strat-001-scenario-map-graph-state,
    production/stories/story-strat-002-hotseat-turn-ownership,
    production/stories/story-strat-003-champion-route-movement,
    production/stories/story-strat-vis-001-minimal-strategic-map-presentation,
    production/stories/story-strat-input-001-select-champion-and-route-move,
    production/stories/story-strat-ui-001-minimal-hotseat-hud,
    production/stories/story-loop-001-minimal-local-hotseat-strategic-loop-smoke,
    production/stories/story-qa-001-strategic-smoke-cleanup-readability-bugfix-pass,
    production/stories/story-tac-001-battle-setup-result-dto-contracts,
    production/stories/story-qa-002-strategic-map-readability-actor-clarity-fix-pass,
  ]
approval: approved
---

# Strategic MVP Story Train 001

## Purpose

Define the first safe Codex implementation train after STORY-STRAT-001, with an explicit bias toward making the strategic loop visible and player-testable as early as possible.

The goal is to increase Codex utilization without giving it a broad, drift-prone mandate. Codex should implement one READY story at a time, on one branch/PR at a time, with CI and review before continuing. Crude visual/input/HUD stories are intentionally inserted before deeper site/battle work so humans can test the local-hotseat movement/end-turn loop early.

## Sequence

| Order | Story                                                                                                                                            | Status                                                              | Why now                                                                                                               | Stop before next if                                                                                                           |
| ----: | ------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------- |
|     0 | [STORY-STRAT-001 Scenario Map Graph State](../stories/story-strat-001-scenario-map-graph-state.md)                                               | Implemented/reviewed in Unity branch; design story remains approved | Foundation state/validation already exists                                                                            | PR not merged or CI/review regresses                                                                                          |
|     1 | [STORY-STRAT-002 Hotseat Turn Ownership](../stories/story-strat-002-hotseat-turn-ownership.md)                                                   | READY                                                               | Turns give all later actions an owner and cadence                                                                     | CI fails, turn rules require UX/design invention, or scope leaks into income/site behavior                                    |
|     2 | [STORY-STRAT-003 Champion Route Movement](../stories/story-strat-003-champion-route-movement.md)                                                 | READY                                                               | Movement makes the graph playable while staying pure domain                                                           | CI fails, pathfinding/modifiers/UI are needed, or turn ownership is unresolved                                                |
|     3 | [STORY-STRAT-VIS-001 Minimal Strategic Map Presentation](../stories/story-strat-vis-001-minimal-strategic-map-presentation.md)                   | READY                                                               | Make the map visible early with crude nodes/routes/Champion markers before deeper invisible systems accumulate        | CI fails, scene/prefab wiring is unsafe, presentation needs architecture/package changes, or visuals imply final art/content  |
|     4 | [STORY-STRAT-INPUT-001 Select Champion and Route Move](../stories/story-strat-input-001-select-champion-and-route-move.md)                       | READY                                                               | Wire the first direct player action: select active Champion and move one adjacent route                               | CI fails, input requires package/settings changes, invalid moves bypass domain services, or scope leaks into site interaction |
|     5 | [STORY-STRAT-UI-001 Minimal Hotseat HUD](../stories/story-strat-ui-001-minimal-hotseat-hud.md)                                                   | READY                                                               | Make hotseat turns understandable and add End Turn so a human can play without developer guidance                     | CI fails, UI requires final UI architecture/art/localization decisions, or End Turn bypasses domain rules                     |
|     6 | [STORY-LOOP-001 Minimal Local Hotseat Strategic Loop Smoke](../stories/story-loop-001-minimal-local-hotseat-strategic-loop-smoke.md)             | Implemented/merged in Unity PR #9                                   | Confirm the crude two-faction movement/end-turn loop is actually player-testable in Unity                             | Smoke cannot be completed, domain/visual/HUD state disagree, or manual/PlayMode evidence is missing                           |
|     7 | [STORY-QA-001 Strategic Smoke Cleanup, Readability, and Bugfix Pass](../stories/story-qa-001-strategic-smoke-cleanup-readability-bugfix-pass.md) | Implemented/merged in Unity PR #10                                  | First playable loop exposed readability/layout/map-feedback problems; fix those before deeper systems hide the issues | Fixes require final UI architecture/art, scope leaks into new gameplay systems, or evidence is missing                        |
|     8 | [STORY-TAC-001 Battle Setup Result DTO Contracts](../stories/story-tac-001-battle-setup-result-dto-contracts.md)                                 | Implemented/merged in Unity PR #11                                  | DTO boundary unblocks guarded-site and result-application stories after the first visible loop is testable            | CI fails or tactical internals are required beyond DTO shape                                                                  |
|     9 | [STORY-QA-002 Strategic Map Readability and Actor-Clarity Fix Pass](../stories/story-qa-002-strategic-map-readability-actor-clarity-fix-pass.md)  | READY-candidate / approval pending                                  | User feedback says controls overlap, screen is crumpled, acting side is unclear, and map action feedback is hard to read | Fixes require final UI architecture/art/localization, scope leaks into new gameplay systems, or evidence is missing        |

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

READY for completed train through STORY-TAC-001. Human approval recorded on 2026-06-02 for STORY-STRAT-002, STORY-STRAT-003, STORY-STRAT-VIS-001, STORY-STRAT-INPUT-001, STORY-STRAT-UI-001, and STORY-LOOP-001. Human approval recorded on 2026-06-03 for STORY-QA-001; Unity PR #10 merged on 2026-06-03. Human approval recorded on 2026-06-03 for STORY-TAC-001; Unity PR #11 merged on 2026-06-03. STORY-QA-002 is drafted as the next READY-candidate cleanup packet and requires explicit human approval before Codex implementation.
