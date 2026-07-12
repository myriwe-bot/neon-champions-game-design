---
title: STORY-UI-SHELL-001 Map-First Strategic UI and Normal Player Shell
type: story
status: ready
phase: production
owner: shared
created: 2026-07-12
updated: 2026-07-12
approval: approved
related: [production/epics/epic-016-accelerated-playable-product-foundation, design/ux/player-shell, docs/architecture/unity-technical-scheme]
---

# STORY-UI-SHELL-001 Map-First Strategic UI and Normal Player Shell

## Value

As a player, I want a normal map-first shell with clear turn, resources, objective, selection, context actions, and feedback so I can play the strategic loop without reading developer diagnostics.

## In scope

- Create normal title/scenario-start/faction-choice entry into the existing authored scenario.
- Replace the default strategic debug surface with the approved shell hierarchy: top bar, map-dominant viewport, selection panel, context action bar, Feed rail, and end-turn control.
- Present Credits, Materials, Intel, active faction/Champion, cycle/turn, objective pressure, movement/action state, army summary, and contextual site/base actions using plain labels.
- Explain disabled actions with a concise reason.
- Move raw IDs and diagnostics behind an explicit debug-overlay toggle, off by default.
- Decompose only touched presentation/orchestration code into bounded views/presenters/view-models or equivalent project-consistent components.
- Preserve current strategic rules, scenario data, AI, tactical handoff, and tests.

## Out of scope

Base-screen final art; tactical shell replacement; new gameplay rules; save/load; full settings/remapping; final accessibility pass; final assets; broad bootstrap rewrite; UI framework migration unless separately approved by spike.

## Acceptance criteria

- Given a clean launch, a player can start the proof scenario and choose HRC or QXZ without debug controls.
- Active faction, Champion, resources, cycle/turn, objective pressure, selection, army summary, legal actions, and end turn are readable at 1080p.
- Selecting empty map, Champion, site, and base produces correct bounded context without stale panels.
- Disabled actions state why; legal action results are visible.
- Raw IDs/diagnostics do not appear in normal mode and remain available through a debug toggle.
- Existing movement, recruitment, construction, end-turn, AI, engagement, and tactical-handoff behavior remains green.
- Automated PlayMode journey covers launch -> faction choice -> select -> move/interact or inspect -> end turn; screenshot evidence covers normal and debug modes.

## Verification

EditMode tests for presentation-state mapping where logic exists; PlayMode journey and regression smoke; 1080p screenshots; exact-head and post-merge Unity CI; manual five-second hierarchy review; PR omissions statement.

## Ambiguity gate

PASS. The Product Constitution, multi-reference player-shell direction, provisional HRC/QXZ identity contract, and proof scenario structure were human-approved on 2026-07-12. Before coding, inspect current Unity presentation boundaries; if implementation would require a UI framework migration, broad architecture rewrite, or gameplay-rule change, stop and report the conflict rather than inventing authority.

## Proposed branch

`story/STORY-UI-SHELL-001-map-first-player-shell`

## Verdict

READY. Human-approved for implementation on 2026-07-12.
