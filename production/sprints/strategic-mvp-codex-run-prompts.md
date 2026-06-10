---
title: Strategic MVP Codex Run Prompts
type: agent-instructions
status: approved
phase: production
owner: shared
created: 2026-06-02
updated: 2026-06-10
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
    production/sprints/strategic-mvp-closeout-story-train-002,
    production/stories/story-strat-004-site-interaction-and-guarded-battle-trigger,
    production/stories/story-tac-002-minimal-hex-board-and-stack-placement,
    production/stories/story-tac-003-minimal-tactical-movement-and-attack-resolution,
    production/stories/story-tac-vis-001-minimal-tactical-board-presentation-and-handoff-switch,
    production/stories/story-tac-004-minimal-battle-end-and-result-return,
    production/stories/story-strat-005-strategic-battle-result-application,
    production/stories/story-loop-002-visible-guarded-site-capture-smoke,
    production/stories/story-tac-005-basic-tactical-player-controls,
    production/stories/story-map-001-larger-two-base-strategic-map-slice,
    production/stories/story-strat-006-simple-recruitment-site-fixed-offer,
    production/stories/story-loop-003-larger-map-recruitment-and-neutral-capture-vertical-slice,
    production/stories/story-tac-006-multi-stack-attacker-tactical-setup,
    production/stories/story-qa-003-loop-slice-visual-readability-and-clickable-layout-pass,
    production/stories/story-qa-004-playability-map-scale-zoom-and-ui-clarity-pass,
  ]
approval: approved
---

# Strategic MVP Codex Run Prompts

## Recommended mode

`STORY-QA-004 Playability Map Scale, Zoom, and UI Clarity Pass` is the current READY / approved Unity implementation packet. Human closeout review rejected the current usability/readability state after QA-003 and hotfix PR #26: map still tiny/unreadable, labels overlap, text obstructs buttons, no zoom/focus, clicked object is unclear, and button meaning is unclear.

Run exactly the checked-in prompt file below; keep the packet focused on map scale/readability, zoom/focus, non-overlapping labels, unobstructed action controls, selected/clicked feedback, and tactical move/attack clarity. Do not add new gameplay systems or final UI/art.

## Copy-safe prompt-file mode

If PowerShell shows `>>`, the here-string was not closed correctly. Avoid here-strings entirely and run Codex from checked-in prompt files instead.

Current prompt-file command:

```powershell
cd C:\Users\NordicGamer\CodexProjects\neon-champions-game-design
git pull --ff-only origin main

# Verify STORY-QA-004 is READY/approved before running Codex.
Select-String -Path production\stories\story-qa-004-playability-map-scale-zoom-and-ui-clarity-pass.md -Pattern "status: ready","approval: approved","Status: PASS"

cd C:\Users\NordicGamer\CodexProjects\neon-champions-unity
git fetch origin
git checkout main
git pull --ff-only origin main
git status --short

$prompt = Get-Content -Raw "C:\Users\NordicGamer\CodexProjects\neon-champions-game-design\production\sprints\codex-story-qa-004.prompt.txt"
codex exec --sandbox workspace-write $prompt

# Trusted-repo fallback if workspace-write is blocked:
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

## Current Prompt A — STORY-QA-004 playability map scale, zoom, and UI clarity

Use the checked-in prompt file:

```powershell
$prompt = Get-Content -Raw "C:\Users\NordicGamer\CodexProjects\neon-champions-game-design\production\sprints\codex-story-qa-004.prompt.txt"
codex exec --sandbox workspace-write $prompt

# Trusted-repo fallback if workspace-write is blocked:
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
- `production/sprints/codex-story-qa-002.prompt.txt`
- `production/sprints/codex-story-strat-004.prompt.txt`
- `production/sprints/codex-story-tac-002.prompt.txt`
- `production/sprints/codex-story-tac-003.prompt.txt`
- `production/sprints/codex-story-tac-vis-001.prompt.txt`
- `production/sprints/codex-story-tac-004.prompt.txt`
- `production/sprints/codex-story-strat-005.prompt.txt`
- `production/sprints/codex-story-loop-002.prompt.txt`
- `production/sprints/codex-story-tac-005.prompt.txt`
- `production/sprints/codex-story-map-001.prompt.txt`
- `production/sprints/codex-story-strat-006.prompt.txt`
- `production/sprints/codex-story-loop-003.prompt.txt`
- `production/sprints/codex-story-tac-006.prompt.txt`
- `production/sprints/codex-story-qa-003.prompt.txt`
- `production/sprints/codex-next-step-epic-closeout.prompt.txt`

Current approved prompt:

- `production/sprints/codex-story-qa-004.prompt.txt`

## After Codex finishes

Codex should commit and push `story/STORY-QA-004-playability-map-scale-zoom-ui-clarity`, then open or prepare a PR titled `STORY-QA-004 Playability map scale, zoom, and UI clarity pass`. Review the PR against the story contract, before/after evidence package, CI, and omissions before merging.
