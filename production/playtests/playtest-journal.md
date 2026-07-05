---
title: Playtest Journal
type: playtest
status: active
phase: production
owner: shared
created: 2026-07-05
updated: 2026-07-05
source_lore: []
related:
  [
    production/stories/story-playtest-001-playtest-journal-and-gate-hook,
    production/epics/epic-vslice-mvp-015-post-audit-foundation-pivot-and-reconciliation,
    production/gates/review-mode,
    production/gates/gate-template,
    docs/architecture/testing-strategy,
  ]
approval: approved
---

# Playtest Journal

## Purpose

This journal makes playtest feel notes first-class production evidence. Use it for human/director playtests, agent-run closeout reviews, and any subjective readability/fun verdict that would otherwise live only in chat.

Recorded notes are source authority for future repair stories when they preserve exact player complaints. Do not smooth sharp complaints into generic UX language.

## Rules

- Keep dated entries append-only unless correcting a factual link/commit typo.
- Preserve exact human complaints in quotes when available.
- Separate observed player friction from proposed fixes.
- Link the build/commit, scenario, story/epic under review, and evidence path.
- Every closeout/playtest story must link one or more journal entries, or explicitly state why playtest evidence is N/A.
- Terse notes are valid. A short exact complaint is better than a polished paraphrase.

## Dated entry template

Copy this section for each playtest.

```markdown
## [YYYY-MM-DD] <story/epic/build> — <short verdict>

- Build / commit / PR:
- Scenario / mode:
- Tester / role:
- Story / epic under review:
- Evidence path / screenshots / video:

### What dragged

- 

### What surprised

- 

### What confused

- 

### What felt off-fiction

- 

### Exact complaints to preserve

- "..."

### Fun verdict

Choose one and add a sentence:

- KEEP — works well enough; continue.
- REVISE — promising but needs a narrow repair.
- REJECT — does not prove the intended experience.
- RETEST — evidence was inconclusive or setup was invalid.

### Next decision

- Close story/epic:
- One narrow follow-up:
- Broader direction decision:
- N/A with reason:
```

## Gate summary format

When a gate or closeout story references playtest evidence, summarize it like this:

```markdown
Playtest evidence:
- Journal entry: `production/playtests/playtest-journal.md#[YYYY-MM-DD]-...`
- Build / commit:
- Verdict: KEEP / REVISE / REJECT / RETEST
- Exact preserved complaints, if any:
  - "..."
- Gate consequence:
```

## Existing preserved complaint seeds

These are not retroactive full journal entries; they are exact complaint seeds already used as acceptance authority before the journal existed. Future entries should quote the relevant dated playtest section instead of scattering complaint text across stories.

### STORY-QA-004 map scale / zoom / UI clarity

Source: `production/stories/story-qa-004-playability-map-scale-zoom-and-ui-clarity-pass.md`.

- "The strategic map is still tiny and unreadable."
- "Text labels overlap themselves."
- "Buttons are obstructed by text."
- "The prototype is very confusing."
- "There is no zoom."
- "It is hard to understand what is clicked."
- "It is hard to understand what buttons do."

### STORY-QA-006 state/action feedback readability

Source: `production/stories/story-qa-006-strategic-tactical-state-action-feedback-readability-pass.md`.

- Strategic turn ownership: “Not really” clear whose turn it is.
- Strategic position/state: selected Champion is visible, but with some nodes “it is unclear” where the Champion is.
- Reachability: mostly visible, but route/node meaning is only “somewhat” clear.
- Guard/site state: guarded vs unguarded is unclear; site/objective state is not meaningful enough.
- Turn changes: “I am unsure what changes each turn.”
- Tactical current actor: “No” — the active stack is not clear, and both stacks appear selectable.
- Tactical sides/targets: friendly vs enemy is “not really” clear; legal attacks are not clear; attacking feels like selecting the other army.
- Tactical results: attack/damage/result feedback is not understood.
- Champion Command: ability availability is visible, but what abilities do and why denials happen is not understood.
- UX blockers explicitly selected: clickable affordances, denial reasons, result feedback, and battle completion/attack understanding.

### EPIC-008 / STORY-ARMY-005 army and recruitment readability

Source: `production/epics/epic-vslice-mvp-008-faction-armies-recruitment-and-tactical-role-identity.md` and `production/stories/story-army-005-army-recruitment-and-map-readability-repair.md`.

- "I would not know how to create a composition or how to view it, so no. It is completely unreadable right now."
- UI is still hard to read and cluttered.
- Dark top-screen hue hurts objective readability.
- Map cannot be moved/panned, making focus annoying.
- Player cannot see or understand their army, units, stacks, roles, or composition.
- Recruitment/dwellings only say “recruited” and do not explain unit type/count/cost/future dwelling model.
- Tactical roles and stack differences are invisible.

### STORY-UX-002 tactical scale / resources / stack clarity

Source: `production/stories/story-ux-002-tactical-playability-scale-resource-hud-and-stack-clarity.md`.

- "Resource use is unclear, resources are not displayed anywhere."
- "Unit stacks also unclear."
- "Tactical area still small."
- "central objective situation seems broken - champion is directed away from the point. Holding is not possible."
- ""Engage CHampion" option is incorrectly displayed there. Cannot attack guard or take control over objective."
- "Also, champion-on-champion combat is not working."

### STORY-QA-007 Champion encounter initiation clarity

Source: `production/stories/story-qa-007-champion-encounter-initiation-clarity.md`.

- Moving into the same area does not clearly trigger battle.
- Movement may be blocked.
- Enemy Champion interaction can feel like selecting the other Champion.

### STORY-CMD-005 command explanation

Source: `production/stories/story-cmd-005-champion-command-explanation-pass.md`.

- Rally Order availability is visible, but what it does is unclear.
- Rally Order denial/result is not understood.
- Drone Strike availability is visible, but what it does and target meaning are unclear.
- Second-use denial is not understood.
- Rally Order and Drone Strike do not yet feel differentiated.
- Marshal vs Operator identity is not yet clear.
