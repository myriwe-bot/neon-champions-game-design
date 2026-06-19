---
title: Strategic MVP Codex Run Prompts
type: agent-instructions
status: approved
phase: production
owner: shared
created: 2026-06-02
updated: 2026-06-19
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
    production/stories/story-obj-001-scenario-objective-state-and-victory-feedback,
    production/stories/story-obj-002-guarded-site-defender-strength-tiers,
    production/stories/story-tac-007-simple-stack-strength-persistence,
    production/stories/story-tac-008-champion-vs-champion-tactical-encounter-path,
    production/stories/story-loop-004-objective-champion-combat-and-casualty-stakes-smoke,
    production/epics/epic-vslice-mvp-003-scenario-objective-champion-combat-and-casualty-stakes,
    production/epics/epic-vslice-mvp-004-intel-resource-on-ramp,
    production/stories/story-intel-001-faction-intel-and-data-cache-pickup,
    production/stories/story-intel-002-first-intel-spending-sink-field-upgrade,
    production/stories/story-qa-005-playmode-evidence-artifact-hygiene,
    production/epics/epic-vslice-mvp-005-champion-command-and-operations-on-ramp,
    production/stories/story-cmd-001-champion-command-archetype-state-and-tactical-hud,
    production/stories/story-cmd-002-first-marshal-and-operator-command-pair,
    production/stories/story-cmd-003-command-on-ramp-closeout-smoke,
    production/stories/story-cmd-004-tactical-command-usability-and-targeting-pass,
    production/sprints/epic-005-playability-repair-train,
    production/stories/story-qa-006-strategic-tactical-state-action-feedback-readability-pass,
    production/stories/story-qa-007-champion-encounter-initiation-clarity,
    production/stories/story-cmd-005-champion-command-explanation-pass,
    production/stories/story-strat-objective-001-multi-turn-objective-contest-direction,
    production/stories/story-tac-ap-001-minimal-tactical-ap-and-defend-state,
    production/stories/story-tac-ai-001-neutral-guard-one-step-combat-ai,
    production/stories/story-strat-read-002-strategic-map-readability-pass,
    production/stories/story-strat-base-001-starting-hub-reinforcement-preview,
    production/stories/story-strat-map-region-001-region-site-presentation-prototype,
    production/stories/story-qa-008-strategic-map-region-playtest-and-closeout-review,
    production/stories/story-army-001-mvp-faction-unit-definitions-and-roster-seed,
    production/stories/story-army-002-tactical-role-behaviors-and-sensor-lock,
    production/stories/story-army-003-fixed-recruitment-offers-and-army-summary,
  ]
approval: approved
---

# Strategic MVP Codex Run Prompts

## Recommended mode

**Current READY / approved Unity implementation packet:** `STORY-ARMY-003 Fixed Recruitment Offers and Army Summary`. Use the checked-in prompt file below.

`STORY-INTEL-001`, `STORY-INTEL-002`, `STORY-INTEL-003`, `STORY-INTEL-004`, `STORY-UX-001`, `STORY-QA-005`, `STORY-CMD-001`, `STORY-CMD-002`, `STORY-CMD-003`, `STORY-CMD-004`, `STORY-QA-006`, `STORY-QA-007`, `STORY-CMD-005`, `STORY-STRAT-OBJECTIVE-001`, `STORY-TAC-AP-001`, `STORY-TAC-AI-001`, `STORY-STRAT-READ-002`, `STORY-STRAT-BASE-001`, `STORY-STRAT-MAP-REGION-001`, `STORY-QA-008`, `STORY-ARMY-001`, and `STORY-ARMY-002` are DONE / merged. EPIC-008 is in production; ARMY-003 is READY / approved.

## Copy-safe prompt-file mode

If PowerShell shows `>>`, the here-string was not closed correctly. Avoid here-strings entirely and run Codex from checked-in prompt files instead.

Current implementation prompt file: `production/sprints/codex-story-army-003.prompt.txt`. Historical prompt files remain for audit only.

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

## Current approved prompt

Run Codex from the checked-in approved prompt file:

```powershell
$prompt = Get-Content -Raw "C:\Users\NordicGamer\CodexProjects\neon-champions-game-design\production\sprints\codex-story-army-003.prompt.txt"
codex exec --sandbox workspace-write $prompt
```

Trusted-repo fallback for the same approved packet:

```powershell
$prompt = Get-Content -Raw "C:\Users\NordicGamer\CodexProjects\neon-champions-game-design\production\sprints\codex-story-army-003.prompt.txt"
codex exec --sandbox danger-full-access $prompt
```

The prompt preflight must verify `STORY-ARMY-003` is `status: ready`, `approval: approved`, and Ambiguity Check PASS before editing Unity code.

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
- `production/sprints/codex-story-obj-001.prompt.txt`
- `production/sprints/codex-story-obj-002.prompt.txt`
- `production/sprints/codex-story-tac-007.prompt.txt`
- `production/sprints/codex-story-tac-008.prompt.txt`
- `production/sprints/codex-story-loop-004.prompt.txt`
- `production/sprints/codex-story-intel-001.prompt.txt`
- `production/sprints/codex-story-intel-002.prompt.txt`
- `production/sprints/codex-story-intel-003.prompt.txt`
- `production/sprints/codex-story-intel-004.prompt.txt`
- `production/sprints/codex-story-ux-001.prompt.txt`
- `production/sprints/codex-story-qa-005.prompt.txt`
- `production/sprints/codex-story-cmd-001.prompt.txt`
- `production/sprints/codex-story-cmd-002.prompt.txt`
- `production/sprints/codex-story-cmd-003.prompt.txt`
- `production/sprints/codex-story-cmd-004.prompt.txt`
- `production/sprints/codex-story-qa-006.prompt.txt`
- `production/sprints/codex-story-qa-007.prompt.txt`
- `production/sprints/codex-story-cmd-005.prompt.txt`
- `production/sprints/codex-story-strat-objective-001.prompt.txt`
- `production/sprints/codex-story-strat-read-002.prompt.txt`
- `production/sprints/codex-story-strat-base-001.prompt.txt`
- `production/sprints/codex-story-strat-map-region-001.prompt.txt`
- `production/sprints/codex-story-qa-008.prompt.txt`
- `production/sprints/codex-story-army-001.prompt.txt`
- `production/sprints/codex-story-army-002.prompt.txt`

Current approved prompt-file run:

- `production/sprints/codex-story-army-003.prompt.txt`

Guarded decision-brief packet:

- `production/sprints/codex-next-epic-direction-brief.prompt.txt`

## After Codex finishes

After approval, Codex must push `story/STORY-ARMY-003-fixed-recruitment-offers-army-summary` or explicitly report why pushing/PR creation was impossible. Final response must include tests/evidence, PR URL/number if created, CI status or blocker, and omissions/deferred work.
