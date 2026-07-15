---
title: Strategic MVP Codex Run Prompts
type: agent-instructions
status: approved
phase: production
owner: shared
created: 2026-06-02
updated: 2026-07-15
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
    production/stories/story-army-004-composition-consequence-scenario,
    production/stories/story-qa-009-epic-008-playtest-and-closeout-review,
    production/stories/story-army-005-army-recruitment-and-map-readability-repair,
    production/stories/story-qa-010-epic-008-repair-playtest-and-closeout-review,
    production/stories/story-army-006-map-camera-recruitment-and-tactical-stack-interaction-repair,
    production/stories/story-qa-011-epic-008-second-repair-playtest-and-closeout-review,
    production/stories/story-army-007-strategic-map-pan-input-repair,
    production/epics/epic-vslice-mvp-009-strategic-map-geography-bases-and-facility-construction,
    production/stories/story-map-real-001-scenario-authored-strategic-map-shell,
    production/stories/story-base-001-base-definition-and-facility-construction-core,
    production/stories/story-base-002-administration-income-chain-and-recruitment-dwellings,
    production/stories/story-terrain-001-strategic-terrain-tags-and-tactical-layout-family-contract,
    production/stories/story-terrain-002-tactical-layout-definitions-and-deployment-zones,
    production/stories/story-terrain-003-tactical-blockers-and-simple-defensive-terrain,
    production/stories/story-terrain-004-range-threat-and-terrain-readability-pass,
    production/stories/story-terrain-005-strategic-context-to-tactical-battlefield-smoke,
    production/stories/story-qa-013-epic-010-playtest-and-closeout-review,
    production/stories/story-ux-002-tactical-playability-scale-resource-hud-and-stack-clarity,
    production/epics/epic-vslice-mvp-010-terrain-tactical-battlefields-and-map-space-readability,
    production/epics/epic-vslice-mvp-012-intel-leads-and-verification,
    production/stories/story-intel-dirty-001-intel-lead-and-verification-on-ramp,
    production/stories/story-intel-dirty-002-stale-intel-readability,
    production/stories/story-intel-dirty-003-intel-layer-closeout-smoke,
    production/epics/epic-vslice-mvp-013-scenario-pressure-and-victory-readability,
    production/stories/story-pressure-001-objective-pressure-and-victory-readability-smoke,
    production/stories/story-pressure-002-opponent-contest-and-loss-pressure-smoke,
    production/stories/story-qa-014-epic-013-playtest-and-closeout-review,
    production/epics/epic-vslice-mvp-014-tactical-role-counterplay-and-combat-decision-readability,
    production/stories/story-tac-role-001-tactical-role-counterplay-readability-smoke,
    production/stories/story-data-001-static-scenario-data-contract-and-scenario-extraction-prep,
    production/stories/story-playtest-001-playtest-journal-and-gate-hook,
    production/stories/story-gate-001-hollow-gate-and-source-truth-reconciliation,
    production/stories/story-determinism-001-determinism-and-rng-decision-record,
    production/stories/story-ai-001-dumb-strategic-ai-playtest-opponent,
    production/stories/story-art-look-001-vertical-look-and-asset-provenance-integration-spike,
    production/stories/story-base-content-001-hrc-qxz-six-facility-prototype-content-and-base-presentation,
    production/stories/story-faction-composition-001-three-line-faction-composition-and-tactical-identity-proof,
    production/stories/story-proof-scenario-001-month-one-route-pressure-feed-and-capture-flow,
  ]
approval: approved
---

# Strategic MVP Codex Run Prompts

## Recommended mode

**Current READY / approved Unity implementation packet:** `STORY-PROOF-SCENARIO-001 Month-One Route, Pressure, Feed, and Capture Flow`.

`STORY-FACTION-COMPOSITION-001` is DONE / merged through Unity PR #155 with post-merge CI passed. `STORY-PROOF-SCENARIO-001` was explicitly approved on 2026-07-15 and is the sole active implementation packet.

## Current READY implementation packet

Use `production/sprints/codex-story-proof-scenario-001.prompt.txt`. Its preflight requires the READY/approved story, source-authority matrix closure, and matching Unity README current-task pointer.

### Copy-safe STORY-PROOF-SCENARIO-001 handoff

Primary workspace-write run:

```powershell
cd C:\Users\NordicGamer\CodexProjects\neon-champions-game-design
git checkout main
git pull --ff-only origin main

cd C:\Users\NordicGamer\CodexProjects\neon-champions-unity
git checkout main
git pull --ff-only origin main
git status --short

$prompt = Get-Content -Raw "C:\Users\NordicGamer\CodexProjects\neon-champions-game-design\production\sprints\codex-story-proof-scenario-001.prompt.txt"
$prompt | codex exec --sandbox workspace-write
```

Trusted-repo fallback:

```powershell
$prompt | codex exec --sandbox danger-full-access
```

Do not rerun the completed faction-composition handoff. Pull both repositories before starting this current packet.

## Most recently completed implementation prompt

Historical completed prompt: `production/sprints/codex-story-faction-composition-001.prompt.txt` for the merged three-line faction-composition story.

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
- `production/sprints/codex-story-intel-dirty-001.prompt.txt`
- `production/sprints/codex-story-intel-dirty-002.prompt.txt`
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
- `production/sprints/codex-story-army-003.prompt.txt`
- `production/sprints/codex-story-army-004.prompt.txt`
- `production/sprints/codex-story-qa-009.prompt.txt`

Most recent completed prompt-file run:

- `production/sprints/codex-story-army-007.prompt.txt`

Historical decision-brief prompt-file run:

- `production/sprints/codex-next-epic-direction-brief.prompt.txt`

Most recent completed prompt-file run:

- `production/sprints/codex-story-map-real-001.prompt.txt`

Most recent completed prompt-file run:

- `production/sprints/codex-story-base-001.prompt.txt`

Most recent completed runnable prompt-file run:

- `production/sprints/codex-story-base-002.prompt.txt`

## Copy-safe STORY-TERRAIN-001 handoff

Primary workspace-write run:

```powershell
cd C:\Users\NordicGamer\CodexProjects\neon-champions-game-design
git checkout main
git pull --ff-only origin main

cd C:\Users\NordicGamer\CodexProjects\neon-champions-unity
git checkout main
git pull --ff-only origin main
git status --short

Get-Content -Raw "C:\Users\NordicGamer\CodexProjects\neon-champions-game-design\production\sprints\codex-story-terrain-001.prompt.txt" | codex exec --sandbox workspace-write
```

Trusted-repo fallback:

```powershell
Get-Content -Raw "C:\Users\NordicGamer\CodexProjects\neon-champions-game-design\production\sprints\codex-story-terrain-001.prompt.txt" | codex exec --sandbox danger-full-access
```

## After Codex finishes

Codex should produce a PR for `STORY-TERRAIN-001`; review against the story acceptance criteria and require exact-head Unity Foundation CI before merge.

## Copy-safe STORY-TERRAIN-003 handoff

Use:

```powershell
cd C:\Users\NordicGamer\CodexProjects\neon-champions-game-design
git checkout main
git pull --ff-only origin main

cd C:\Users\NordicGamer\CodexProjects\neon-champions-unity
git checkout main
git pull --ff-only origin main
git status --short

Get-Content -Raw "C:\Users\NordicGamer\CodexProjects\neon-champions-game-design\production\sprints\codex-story-terrain-003.prompt.txt" | codex exec --sandbox workspace-write
```

Trusted-repo fallback:

```powershell
Get-Content -Raw "C:\Users\NordicGamer\CodexProjects\neon-champions-game-design\production\sprints\codex-story-terrain-003.prompt.txt" | codex exec --sandbox danger-full-access
```

## Copy-safe STORY-TERRAIN-004 handoff

Use:

```powershell
cd C:\Users\NordicGamer\CodexProjects\neon-champions-game-design
git checkout main
git pull --ff-only origin main

cd C:\Users\NordicGamer\CodexProjects\neon-champions-unity
git checkout main
git pull --ff-only origin main
git status --short

Get-Content -Raw "C:\Users\NordicGamer\CodexProjects\neon-champions-game-design\production\sprints\codex-story-terrain-004.prompt.txt" | codex exec --sandbox workspace-write
```

Trusted-repo fallback:

```powershell
Get-Content -Raw "C:\Users\NordicGamer\CodexProjects\neon-champions-game-design\production\sprints\codex-story-terrain-004.prompt.txt" | codex exec --sandbox danger-full-access
```

## Copy-safe STORY-TERRAIN-005 handoff

Use:

```powershell
cd C:\Users\NordicGamer\CodexProjects\neon-champions-game-design
git checkout main
git pull --ff-only origin main

cd C:\Users\NordicGamer\CodexProjects\neon-champions-unity
git checkout main
git pull --ff-only origin main
git status --short

Get-Content -Raw "C:\Users\NordicGamer\CodexProjects\neon-champions-game-design\production\sprints\codex-story-terrain-005.prompt.txt" | codex exec --sandbox workspace-write
```

Trusted-repo fallback:

```powershell
Get-Content -Raw "C:\Users\NordicGamer\CodexProjects\neon-champions-game-design\production\sprints\codex-story-terrain-005.prompt.txt" | codex exec --sandbox danger-full-access
```

## Copy-safe STORY-QA-013 handoff

Use:

```powershell
cd C:\Users\NordicGamer\CodexProjects\neon-champions-game-design
git checkout main
git pull --ff-only origin main

cd C:\Users\NordicGamer\CodexProjects\neon-champions-unity
git checkout main
git pull --ff-only origin main
git status --short

Get-Content -Raw "C:\Users\NordicGamer\CodexProjects\neon-champions-game-design\production\sprints\codex-story-qa-013.prompt.txt" | codex exec --sandbox workspace-write
```

Trusted-repo fallback:

```powershell
Get-Content -Raw "C:\Users\NordicGamer\CodexProjects\neon-champions-game-design\production\sprints\codex-story-qa-013.prompt.txt" | codex exec --sandbox danger-full-access
```

## Copy-safe STORY-UX-002 handoff

Use stdin piping instead of passing prompt contents as an argv argument. On the Windows Codex shim, large/multiline prompt arguments can still be split or reparsed and produce errors like `unexpected argument 'use' found`.

Primary workspace-write run:

```powershell
cd C:\Users\NordicGamer\CodexProjects\neon-champions-game-design
git checkout main
git pull --ff-only origin main

cd C:\Users\NordicGamer\CodexProjects\neon-champions-unity
git checkout main
git pull --ff-only origin main
git status --short

Get-Content -Raw "C:\Users\NordicGamer\CodexProjects\neon-champions-game-design\production\sprints\codex-story-ux-002.prompt.txt" | codex exec --sandbox workspace-write
```

Trusted-repo fallback:

```powershell
Get-Content -Raw "C:\Users\NordicGamer\CodexProjects\neon-champions-game-design\production\sprints\codex-story-ux-002.prompt.txt" | codex exec --sandbox danger-full-access
```

## Final control-surface state

`STORY-PROOF-SCENARIO-001` is the sole current READY / approved Unity implementation packet. `STORY-FACTION-COMPOSITION-001` remains historical and DONE.
