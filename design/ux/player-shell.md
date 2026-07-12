---
title: Player Shell and UI Reference Synthesis
type: ux-spec
status: approved
phase: pre-production
owner: shared
created: 2026-07-12
updated: 2026-07-12
approval: approved
related: [design/research/zero-budget-prototype-assets-and-reference-games-2026-07-12, design/gdd/product-constitution]
---

# Player Shell and UI Reference Synthesis

## Direction

The shell is not “Civilization V UI.” It combines lessons from several references while preserving a distinct White Sky cyberpunk identity. No single game owns the layout.

Human-approved on 2026-07-12 as a testable direction. Exact layouts remain subject to implementation evidence and playtesting rather than permanent lock.

## Reference responsibilities

| Reference | Borrow the lesson | Do not copy |
|---|---|---|
| Civilization V | calm authority, map dominance, top-level resource/turn clarity, tactile end-turn cadence | empire-scale clutter or hex assumptions |
| Heroes III | immediate resource language, map desire, site/town anticipation, low-friction turn flow | opaque legacy interaction |
| Olden Era | modern HoMM hierarchy, contemporary town/faction presentation | provisional details treated as settled standards |
| Songs of Conquest | compact modern adventure-map UI, settlement growth readability, commander/army relationship | pixel-art skin or exact panel arrangement |
| XCOM | action economy, selection state, forecast and consequence clarity | percent-hit/cover model by default |
| Into the Breach | explicit intent, previewed consequences, objective tradeoffs | puzzle-board reduction of uncertainty |
| Invisible, Inc. | fair uncertainty, threat communication, clean cyberpunk information design | stealth-game screen grammar wholesale |
| Shadowrun Returns | constrained-budget cyberpunk cohesion, portraits, readable dialogue/event delivery | text-heavy exposition |
| Jagged Alliance 3 | character/army continuity across strategic and tactical layers | inventory/micro-management breadth |
| BATTLETECH | consequential maintenance and damage presentation | routine upkeep chores and dense mech simulation |

## Global principles

1. Map or battlefield remains visually dominant.
2. Persistent UI shows only current resources, turn/faction, objective pressure, and critical alerts.
3. Selection reveals context; it does not open a permanent debug wall.
4. Every action shows legality, cost, expected consequence, and reason when denied.
5. Feed/narrative events interrupt proportionally: toast -> expandable card -> dedicated scene only when earned.
6. Faction expression uses silhouette, icon grammar, motion, sound, and controlled accents—not recolored identical chrome.
7. Raw IDs and diagnostic state are restricted to a toggleable debug overlay.

## Strategic shell

- Top bar: Credits, Materials, Intel; cycle/turn; faction/Champion identity; compact objective pressure.
- Map: routes, reachable state, ownership, site type, threat, and information reliability through layered visual language.
- Selection panel: portrait/silhouette, army summary, movement/action state, current context.
- Context action bar: only legal or explainably disabled actions; construction, recruitment, inspect, interact.
- End-turn control: prominent, tactile, includes unresolved-critical-action warning without nagging.
- Feed rail: recent consequences and information provenance, expandable but not permanently dominant.

## Base screen/panel

Town anticipation from HoMM/Songs of Conquest, presented with Civilization-like restraint: six visible facility slots/cards, clear prerequisites/costs, one-build-per-cycle state, visual base change, and faction-specific benefits stated in plain language.

## Tactical shell

XCOM/Into the Breach clarity with HoMM stack identity: initiative/activation state, unit line and count/strength, AP, movement/attack affordances, target forecast, terrain/objective state, and concise combat event feed. Champion actions remain distinct from ordinary unit actions.

## Required states

Title/start; scenario briefing and faction choice; strategic map; base construction; engagement preview; tactical battle; Feed consequence; pause/settings; victory/defeat; loading/error/recovery; debug overlay off by default.

## Accessibility baseline

Keyboard/mouse navigation, scalable text, contrast-safe state encoding beyond color, captions/subtitles, independent audio controls, reduced motion option, and no essential information conveyed only by animation.

## Four-week proof acceptance criteria

- A new player can start, choose HRC/QXZ, identify objective/resources/turn, select and move, inspect/build at a base, recruit or understand why unavailable, enter combat, predict a legal action, and recognize victory/defeat without raw IDs or live explanation.
- Strategic and tactical screenshots are understandable at normal capture resolution.
- Debug overlay can be enabled for development without changing normal layout.
- Reference influence is visible as synthesis, not imitation.
