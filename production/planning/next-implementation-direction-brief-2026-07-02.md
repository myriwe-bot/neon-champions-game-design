---
title: Next Implementation Direction Brief — 2026-07-02
type: decision-brief
status: approved
phase: production
owner: shared
created: 2026-07-02
updated: 2026-07-02
related:
  - production/epics/epic-vslice-mvp-013-scenario-pressure-and-victory-readability
  - production/stories/story-qa-014-epic-013-playtest-and-closeout-review
  - design/gdd/strategic-map
  - design/gdd/tactical-combat
  - design/gdd/intel-resource
approval: approved
---

# Next Implementation Direction Brief — 2026-07-02

## State

`EPIC-VSLICE-MVP-013 Scenario Pressure and Victory Readability` is DONE / closed for the approved MVP slice. Unity PR #133 merged as `9e27b6b63abda739392f10af3a9d5adf97fa4a16`; exact-head PR CI and post-merge `main` CI passed. The closeout verdict was `CLOSE EPIC-013`.

The prototype now has a readable strategic pressure loop: current objective pressure, action feedback, victory direction, opponent contest state, and loss direction are visible in focused PlayMode evidence. No Unity implementation is currently authorized after pointer cleanup; the next implementation direction needs human approval before a READY story/prompt is created.

## Viable next directions

1. **Tactical role counterplay and combat decision readability** — make one tactical choice pattern legible: range, defend, focus-fire, sensor/marked target, retaliation, or simple role interaction, without expanding into full tactical AI or balance.
2. **Strategic economy/base choice depth** — return to base/facility choices and income-chain readability now that objective pressure exists, while avoiding full town-tree sprawl.
3. **Champion operations second slice** — build one more non-magical Champion operation or aftermath consequence, but avoid full spellbook/progression/inventory.
4. **Dirty-information next epic** — explicitly open the next contested/false-lead/PR/counter-intel layer; must not mutate the closed EPIC-012 Intel slice by stealth.

## Recommended default

Recommend **Tactical role counterplay and combat decision readability** as the next implementation direction.

Why:

- The strategic loop is now easier to read; the next weakest core-loop question is whether tactical choices are interesting and understandable once the player enters battle.
- It reinforces the HoMM-like strategy/RPG promise without adding campaign, economy, or broad AI scope.
- It can stay narrow: one tactical role/counterplay smoke, one player-facing decision, focused EditMode/PlayMode evidence, and no final balancing.
- It gives later strategic/economy/Champion systems a more meaningful combat endpoint to point at.

## Suggested first implementation slice if approved

`STORY-TAC-ROLE-001 Tactical Role Counterplay Readability Smoke`:

- Use existing tactical battle setup, unit/stack presentation, AP/defend, retaliation/range-threat/readability surfaces where possible.
- Add or clarify exactly one tactical role decision pattern, such as a marked/sensor-locked target, ranged threat, defend tradeoff, or simple assault/support counter.
- Show the player what choice is available, why it matters, and what happened after the action.
- Add focused EditMode/PlayMode coverage and generated evidence for before-choice, choice-available, action-result, and surrounding-loop-unbroken states.

## Approval gate

Approved 2026-07-02 via user instruction: "approved". Create/approve the narrow parent epic `EPIC-VSLICE-MVP-014 Tactical Role Counterplay and Combat Decision Readability` and first READY story `STORY-TAC-ROLE-001 Tactical Role Counterplay Readability Smoke`, then update the Unity README current-task pointer through a CI-gated docs PR before Codex implementation.
