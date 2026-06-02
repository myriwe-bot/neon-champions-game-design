---
title: Strategic MVP Codex Execution System
type: agent-instructions
status: approved
phase: production
owner: shared
created: 2026-06-02
updated: 2026-06-02
source_lore: []
related: [production/sprints/strategic-mvp-story-train-001, production/stories/story-strat-002-hotseat-turn-ownership, production/stories/story-strat-003-champion-route-movement, production/stories/story-strat-vis-001-minimal-strategic-map-presentation, production/stories/story-strat-input-001-select-champion-and-route-move, production/stories/story-strat-ui-001-minimal-hotseat-hud, production/stories/story-loop-001-minimal-local-hotseat-strategic-loop-smoke]
approval: approved
---

# Strategic MVP Codex Execution System

## Purpose

This is the operating system for Codex implementation of the approved Strategic MVP story train after STORY-STRAT-001.

Codex must implement one READY story at a time, on a dedicated branch, with tests/evidence/PR review before the next story starts. This document is an execution wrapper only; the story files and linked source documents remain authoritative.

## Repositories

Expected local repositories on the implementation machine:

- Unity implementation repo:
  - Windows: `C:\Users\NordicGamer\CodexProjects\neon-champions-unity`
  - Server mirror/reference: `/root/wiki/neon-champions-unity`
- Game design/control repo:
  - Windows: `C:\Users\NordicGamer\CodexProjects\neon-champions-game-design`
  - Server source/reference: `/root/wiki/neon-champions-game-design`

If paths differ, locate repositories by name and keep the same relative paths.

## Approved implementation queue

| Order | Story | Branch | Estimate | Start condition |
|---:|---|---|---|---|
| 1 | `STORY-STRAT-002` Hotseat Turn Ownership | `story/STORY-STRAT-002-hotseat-turn-ownership` | S | STORY-STRAT-001 merged or available on the implementation branch |
| 2 | `STORY-STRAT-003` Champion Route Movement | `story/STORY-STRAT-003-champion-route-movement` | S/M | STORY-STRAT-002 merged |
| 3 | `STORY-STRAT-VIS-001` Minimal Strategic Map Presentation | `story/strat-vis-001-minimal-map-presentation` | M | STORY-STRAT-003 merged or consciously implemented against current domain branch |
| 4 | `STORY-STRAT-INPUT-001` Select Champion and Route Move | `story/strat-input-001-select-route-move` | M | VIS plus STRAT-003 movement service available |
| 5 | `STORY-STRAT-UI-001` Minimal Hotseat HUD | `story/strat-ui-001-minimal-hotseat-hud` | M | STRAT-002 turn service and VIS scene available; INPUT recommended |
| 6 | `STORY-LOOP-001` Minimal Local Hotseat Strategic Loop Smoke | `story/loop-001-hotseat-strategic-smoke` | S/M | STRAT-002, STRAT-003, VIS, INPUT, and UI merged |

`STORY-TAC-001` is not in this immediate implementation queue. Its source authority is clarified, but it remains separate from the first visible strategic loop train unless explicitly approved later.

## Required preflight for every story

From the Unity repo root:

```bash
git fetch origin
git checkout main
git pull --ff-only origin main
git status --short
```

Stop if:

- `main` cannot fast-forward cleanly;
- the working tree has unrelated changes;
- the previous story PR is not merged, unless the human explicitly asks to continue on a stacked branch;
- required design/control files are missing;
- a linked source is draft/pending in a way that would become implementation authority;
- implementation requires package/settings/final architecture/content/lore decisions not authorized by the story.

## Required reading order for every Codex run

1. The READY story file under `neon-champions-game-design/production/stories/`.
2. The parent epic: `production/epics/epic-strat-mvp-001-strategic-mvp-core-loop.md`.
3. Every GDD section named in the story's Source requirements.
4. Every architecture/control source named in the story's Source requirements.
5. `production/sprints/strategic-mvp-story-train-001.md`.
6. This execution system document.
7. Unity repo root `AGENTS.md`.
8. Every scoped Unity repo `AGENTS.md` under touched paths.
9. Existing assembly definitions, test layout, and nearby story implementation patterns.

## Standard Codex prompt

Use a short prompt so Codex reads checked-in files instead of relying on pasted context:

```text
Implement exactly one READY story: <STORY-ID>.

Unity repo: <path-to-neon-champions-unity>
Design/control repo: <path-to-neon-champions-game-design>

Required process:
1. Read the story file, parent epic, all linked GDD/architecture/control docs, production/sprints/strategic-mvp-story-train-001.md, production/sprints/strategic-mvp-codex-execution-system.md, Unity AGENTS.md, and scoped AGENTS.md files before coding.
2. Start from updated main and create/use the exact branch named in the story.
3. Use TDD for production logic: RED test, minimal implementation, GREEN test, refactor only under green tests.
4. Keep changes story-scoped. Do not add unapproved packages, settings changes, final UI/art/content/lore, save/load, tactical combat, site rewards, strategic AI, or hidden gameplay behavior.
5. Run the story-required EditMode/PlayMode/validator/manual checks where available. If a check cannot run, report the exact blocker and do not claim it passed.
6. Commit and push the scoped branch if the sandbox permits it.
7. Open a PR with summary, story ID, source docs read, tests/checks, RED/GREEN evidence, CI status/link, manual evidence if required, and omissions/stubs/mocks/assumptions/deferred work.
8. Stop before starting the next story until CI and review pass and the PR is merged.

Stop and report instead of guessing if sources are missing, draft/pending/contradictory, the repo is dirty, CI fails, or the story would require scope expansion.
```

## Story-specific prompt wrappers

### STORY-STRAT-002

```text
Implement exactly one READY story: STORY-STRAT-002.
Story file: production/stories/story-strat-002-hotseat-turn-ownership.md
Branch: story/STORY-STRAT-002-hotseat-turn-ownership
Primary output: pure domain turn service/controller plus EditMode tests.
Do not implement UI, movement execution, income, site interaction, rewards, battle handoff, or scene changes.
```

### STORY-STRAT-003

```text
Implement exactly one READY story: STORY-STRAT-003.
Story file: production/stories/story-strat-003-champion-route-movement.md
Branch: story/STORY-STRAT-003-champion-route-movement
Primary output: pure domain route movement preview/apply service plus EditMode tests.
Do not implement pathfinding, movement UI/input, site interaction, auto-claim, rewards, or turn automation.
```

### STORY-STRAT-VIS-001

```text
Implement exactly one READY story: STORY-STRAT-VIS-001.
Story file: production/stories/story-strat-vis-001-minimal-strategic-map-presentation.md
Branch: story/strat-vis-001-minimal-map-presentation
Primary output: crude strategic map scene/presentation adapter and smoke evidence.
Do not implement player input, End Turn HUD, tactical battle, final art, package/settings changes, or new gameplay rules.
```

### STORY-STRAT-INPUT-001

```text
Implement exactly one READY story: STORY-STRAT-INPUT-001.
Story file: production/stories/story-strat-input-001-select-champion-and-route-move.md
Branch: story/strat-input-001-select-route-move
Primary output: select active Champion and move one reachable adjacent route through the approved movement service.
Do not mutate domain state directly from input/presentation code. Do not implement End Turn HUD, site interaction, pathfinding, new packages, or final input architecture.
```

### STORY-STRAT-UI-001

```text
Implement exactly one READY story: STORY-STRAT-UI-001.
Story file: production/stories/story-strat-ui-001-minimal-hotseat-hud.md
Branch: story/strat-ui-001-minimal-hotseat-hud
Primary output: crude hotseat HUD plus End Turn control calling the approved turn service.
Do not add final UI architecture, localization framework, resource economy, site/reward/victory behavior, or movement rules.
```

### STORY-LOOP-001

```text
Implement exactly one READY story: STORY-LOOP-001.
Story file: production/stories/story-loop-001-minimal-local-hotseat-strategic-loop-smoke.md
Branch: story/loop-001-hotseat-strategic-smoke
Primary output: integrated smoke scene/checklist/evidence for selecting, moving, ending turn, switching faction, moving, and wrapping round.
Do not add site interaction, battle trigger, rewards, victory, final art, or new architecture beyond light smoke wiring.
```

## PR evidence template

Every implementation PR body must include:

```markdown
## Story
- <STORY-ID> <title>

## Source docs read
- <story file>
- <GDD sections>
- <architecture/control docs>
- Unity AGENTS.md and scoped AGENTS.md files

## Summary
- ...

## Tests / checks
- RED: ...
- GREEN: ...
- Regression: ...
- CI: ...

## Manual evidence
- Required? yes/no
- Link/path/screenshots/video/checklist: ...

## Omissions / stubs / mocks / assumptions / deferred work
- ... or `No known omissions`

## Scope-control confirmation
- No unauthorized packages/settings/final content/lore/architecture/gameplay systems added.
```

## Merge/continue rule

After each PR:

1. Review against the story and control manifest.
2. Confirm CI status.
3. Confirm omissions are explicit.
4. Merge only when the DONE gate is satisfied or a human-approved exception is recorded.
5. Update `main`, then start the next story branch.

No parallel story implementation in this train unless the human explicitly approves a stacked/parallel branch plan.
