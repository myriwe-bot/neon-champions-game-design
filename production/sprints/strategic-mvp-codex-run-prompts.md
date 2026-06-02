---
title: Strategic MVP Codex Run Prompts
type: agent-instructions
status: approved
phase: production
owner: shared
created: 2026-06-02
updated: 2026-06-02
source_lore: []
related: [production/sprints/strategic-mvp-story-train-001, production/sprints/strategic-mvp-codex-execution-system, production/stories/story-strat-002-hotseat-turn-ownership, production/stories/story-strat-003-champion-route-movement]
approval: approved
---

# Strategic MVP Codex Run Prompts

## Recommended mode

Start with `STORY-STRAT-002` only. If it passes tests and opens a PR, review/merge it, then run `STORY-STRAT-003`.

A multi-story Codex run is allowed only for the logic pair `STORY-STRAT-002` + `STORY-STRAT-003`, because both are pure domain/EditMode stories. Codex must still commit them separately and may not continue into visual/input/UI/loop stories in the same run.

## Windows PowerShell preflight

Run this in PowerShell:

```powershell
cd C:\Users\NordicGamer\CodexProjects\neon-champions-game-design
git pull --ff-only origin main

cd C:\Users\NordicGamer\CodexProjects\neon-champions-unity
git fetch origin
git checkout main
git pull --ff-only origin main
git status --short
```

If `git status --short` prints anything, stop and inspect before running Codex.

## Prompt A — preferred single-story start

Use this first:

```powershell
cd C:\Users\NordicGamer\CodexProjects\neon-champions-unity
$prompt = @'
Implement exactly one READY story: STORY-STRAT-002.

Unity repo: C:\Users\NordicGamer\CodexProjects\neon-champions-unity
Design/control repo: C:\Users\NordicGamer\CodexProjects\neon-champions-game-design

Required process:
1. Read, in order:
   - design/control story file: production/stories/story-strat-002-hotseat-turn-ownership.md
   - parent epic: production/epics/epic-strat-mvp-001-strategic-mvp-core-loop.md
   - all GDD and architecture/control docs linked by the story
   - production/sprints/strategic-mvp-story-train-001.md
   - production/sprints/strategic-mvp-codex-execution-system.md
   - production/sprints/strategic-mvp-codex-run-prompts.md
   - Unity repo AGENTS.md and every scoped AGENTS.md under touched paths
   - existing assembly definitions, test layout, and STORY-STRAT-001 implementation patterns
2. Start from updated main and create/use branch:
   story/STORY-STRAT-002-hotseat-turn-ownership
3. Implement only pure domain hotseat turn ownership:
   - turn begin/start service behavior
   - active faction Champion movement/action reset
   - end-turn advancement
   - turn/round increment/wrap behavior
   - invalid-state diagnostics
   - required EditMode tests
4. Use TDD: RED test, minimal implementation, GREEN test, refactor only under green tests.
5. Do not implement UI, scene, input, camera, movement execution, income, site interaction, rewards, battle handoff, strategic AI, save/load, package/settings changes, lore/content, or final data-authoring decisions.
6. Run relevant EditMode tests and any repo validators available. If Unity CLI cannot run, report the exact blocker and do not claim tests passed.
7. Commit and push if sandbox permits.
8. Open a PR titled:
   STORY-STRAT-002 Hotseat turn ownership
9. PR body must include summary, source docs read, RED/GREEN evidence, tests/checks, CI status/link if available, and omissions/stubs/mocks/assumptions/deferred work.

Stop and report instead of guessing if sources are missing, draft/pending/contradictory, the repo is dirty, tests fail, CI fails, or implementation would require scope expansion.
'@
codex exec --sandbox workspace-write $prompt
```

If Codex errors with Windows sandbox setup/spawn issues, rerun only after reviewing trust/scope:

```powershell
codex exec --sandbox danger-full-access $prompt
```

## Prompt B — optional two-story logic batch

Use this only if you want Codex to attempt `STORY-STRAT-002` and `STORY-STRAT-003` in one session. This is more aggressive. It must still keep separate commits and ideally separate PRs/branches.

```powershell
cd C:\Users\NordicGamer\CodexProjects\neon-champions-unity
$prompt = @'
Implement a sequential two-story logic batch: STORY-STRAT-002, then STORY-STRAT-003.

Unity repo: C:\Users\NordicGamer\CodexProjects\neon-champions-unity
Design/control repo: C:\Users\NordicGamer\CodexProjects\neon-champions-game-design

Hard rules:
- Read all required source docs before coding each story.
- Keep story work separable by commit and, if possible, by PR.
- Do not proceed to STORY-STRAT-003 unless STORY-STRAT-002 tests are green and its commit is complete.
- Do not implement STORY-STRAT-VIS-001, STORY-STRAT-INPUT-001, STORY-STRAT-UI-001, STORY-LOOP-001, or STORY-TAC-001 in this run.
- Stop on ambiguity, dirty repo, missing/draft/contradictory authority, test failure you cannot fix story-locally, CI failure, or scope expansion.

Required reading order before STORY-STRAT-002:
1. production/stories/story-strat-002-hotseat-turn-ownership.md
2. production/epics/epic-strat-mvp-001-strategic-mvp-core-loop.md
3. all GDD/architecture/control docs linked by STORY-STRAT-002
4. production/sprints/strategic-mvp-story-train-001.md
5. production/sprints/strategic-mvp-codex-execution-system.md
6. production/sprints/strategic-mvp-codex-run-prompts.md
7. Unity AGENTS.md and scoped AGENTS.md files
8. existing source/test layout and STORY-STRAT-001 implementation patterns

STORY-STRAT-002 branch:
story/STORY-STRAT-002-hotseat-turn-ownership

STORY-STRAT-002 scope:
- pure domain turn begin/end service/controller
- active faction Champion movement/action reset
- turn/round advancement and wrap
- invalid-state diagnostics
- EditMode tests with RED/GREEN evidence
No UI, scene, input, movement execution, income, site, rewards, battle handoff, packages/settings, save/load, lore/content, or AI.

After STORY-STRAT-002 is green and committed, decide how to continue:
- Preferred: push/open PR for STORY-STRAT-002 and stop.
- If local process allows stacked work and no merge is required yet, create/use branch:
  story/STORY-STRAT-003-champion-route-movement
  based on the completed STORY-STRAT-002 branch, and clearly report it as stacked.

Required reading order before STORY-STRAT-003:
1. production/stories/story-strat-003-champion-route-movement.md
2. parent epic and all linked GDD/architecture/control docs
3. same sprint/execution docs and AGENTS.md files
4. existing STRAT-001/STRAT-002 source/test patterns

STORY-STRAT-003 scope:
- pure domain route movement request/preview/apply service
- validation for Champion existence, active faction ownership if available, origin/current node, connected route, positive/affordable route cost, defeated/locked Champion restrictions
- preview must not mutate runtime state
- apply updates current node and movement points only after validation passes
- EditMode tests with RED/GREEN evidence
No pathfinding, UI/input, scene, camera, site interaction, auto-claim, rewards, turn automation, movement modifiers, packages/settings, save/load, lore/content, or AI.

Finish report must include:
- branches/commits created
- whether STORY-STRAT-003 is stacked on STORY-STRAT-002
- files changed per story
- tests/checks run and results
- RED/GREEN evidence per story
- PR URLs if opened
- omissions/stubs/mocks/assumptions/deferred work
- any stop-condition risks
'@
codex exec --sandbox workspace-write $prompt
```

If Codex errors with Windows sandbox setup/spawn issues, rerun only after reviewing trust/scope:

```powershell
codex exec --sandbox danger-full-access $prompt
```

## After Codex finishes

Run this from the Unity repo:

```powershell
git status --short
git log --oneline -5
git branch --show-current
```

If Codex created a branch but did not push:

```powershell
git push -u origin HEAD
```

If Codex did not create a PR and GitHub CLI is available:

```powershell
gh pr create --title "STORY-STRAT-002 Hotseat turn ownership" --body-file .\PR_BODY.md
```

For the optional stacked second story, use the title:

```powershell
gh pr create --title "STORY-STRAT-003 Champion route movement" --body-file .\PR_BODY.md
```
