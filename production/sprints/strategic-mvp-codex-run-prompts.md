---
title: Strategic MVP Codex Run Prompts
type: agent-instructions
status: approved
phase: production
owner: shared
created: 2026-06-02
updated: 2026-06-03
source_lore: []
related:
  [
    production/sprints/strategic-mvp-story-train-001,
    production/sprints/strategic-mvp-codex-execution-system,
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

# Strategic MVP Codex Run Prompts

## Recommended mode

`STORY-TAC-001` is merged. The next proposed packet is `STORY-QA-002`, but it is approval-pending. Use the QA-002 prompt only after the story is explicitly approved.

Keep story work sequential: approve and implement `STORY-QA-002` first if readability remains the priority, then continue to guarded-site/battle/result stories one at a time.

## Copy-safe prompt-file mode

If PowerShell shows `>>`, the here-string was not closed correctly. Avoid here-strings entirely and run Codex from checked-in prompt files instead.

Preferred single-story run:

```powershell
cd C:\Users\NordicGamer\CodexProjects\neon-champions-game-design
git pull --ff-only origin main

cd C:\Users\NordicGamer\CodexProjects\neon-champions-unity
git fetch origin
git checkout main
git pull --ff-only origin main
git status --short

$prompt = Get-Content -Raw "C:\Users\NordicGamer\CodexProjects\neon-champions-game-design\production\sprints\codex-story-qa-002.prompt.txt"
codex exec --sandbox workspace-write $prompt
```

If Codex errors with Windows sandbox setup/spawn issues, rerun the last command with:

```powershell
codex exec --sandbox danger-full-access $prompt
```

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

## Current Prompt A — preferred single-story start

Use this after approving `STORY-QA-002`:

```powershell
cd C:\Users\NordicGamer\CodexProjects\neon-champions-unity
$prompt = Get-Content -Raw "C:\Users\NordicGamer\CodexProjects\neon-champions-game-design\production\sprints\codex-story-qa-002.prompt.txt"
codex exec --sandbox workspace-write $prompt
```

If Codex errors with Windows sandbox setup/spawn issues, rerun only after reviewing trust/scope:

```powershell
codex exec --sandbox danger-full-access $prompt
```

## Historical prompt-file runs

Historical prompt-file runs are retained in this folder for audit only:

- `production/sprints/codex-story-strat-002.prompt.txt`
- `production/sprints/codex-story-strat-003.prompt.txt`
- `production/sprints/codex-story-strat-vis-001.prompt.txt`
- `production/sprints/codex-story-strat-input-001.prompt.txt`
- `production/sprints/codex-story-strat-ui-001.prompt.txt`
- `production/sprints/codex-story-loop-001.prompt.txt`
- `production/sprints/codex-story-qa-001.prompt.txt`
- `production/sprints/codex-story-tac-001.prompt.txt`

Current candidate prompt:

- `production/sprints/codex-story-qa-002.prompt.txt`

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
gh pr create --title "STORY-QA-002 Strategic map readability and actor clarity fix pass" --body-file .\PR_BODY.md
```
