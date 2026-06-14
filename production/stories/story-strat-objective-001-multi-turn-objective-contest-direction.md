---
title: STORY-STRAT-OBJECTIVE-001 Multi-Turn Objective Contest Direction
type: story
status: ready-candidate
phase: production
owner: shared
created: 2026-06-13
updated: 2026-06-14
source_lore: []
related:
  [
    design/gdd/strategic-map,
    production/epics/epic-vslice-mvp-005-champion-command-and-operations-on-ramp,
    production/sprints/epic-005-playability-repair-train,
    production/stories/story-obj-001-scenario-objective-state-and-victory-feedback,
    production/stories/story-obj-002-guarded-site-defender-strength-tiers,
    production/stories/story-loop-004-objective-champion-combat-and-casualty-stakes-smoke,
    production/stories/story-cmd-005-champion-command-explanation-pass,
    docs/architecture/control-manifest,
    docs/architecture/testing-strategy,
    docs/architecture/ci-build-automation,
  ]
approval: pending
---

# STORY-STRAT-OBJECTIVE-001 Multi-Turn Objective Contest Direction

## Status

READY-candidate / approval pending. This is the next named concern after the EPIC-005 readability repair train, but it is design-heavy and is **not** authorized for Codex implementation until human approval resolves the objective rule choices below.

`STORY-CMD-005` is DONE / merged. There is no current approved Unity implementation story after CMD-005.

## Human playtest source

The player reported:

- Objective capture is too easy.
- It is possible to “sneak” the objective.
- In the real game, capture should likely take several turns and possibly several rounds of defenses.
- Guarded vs unguarded state is unclear.

Preserve this complaint as first-class design authority. Do not turn it into generic “make objective harder”.

## Design problem

The current objective is too binary for the intended fantasy of contested cyberpunk territorial struggle. The likely future direction is a multi-turn contest/capture process with clearer defenses, warnings, and counterplay.

## Candidate implementation value

A future implementation story should make objective capture readable and contestable enough that a player can tell:

- who is contesting or controlling the objective;
- how close capture is;
- what defense or counterplay window remains;
- why capture did or did not complete.

## Approval choices required before READY

Choose exactly one first implementation shape:

1. **Two-turn capture countdown** — interacting with the objective starts a visible capture state; the same faction must hold/confirm on a later turn to win. Smallest likely implementation.
2. **Round-based defense waves** — capture triggers one or more required defensive tactical encounters before victory. More dramatic, but larger and riskier.
3. **Contest/control-points model** — factions accumulate or interrupt objective progress over multiple turns. More systemic, best saved for a larger strategic-objective epic.
4. **Clarity-only guard state** — do not change capture timing yet; only make guarded/unguarded and “capture would win now” warnings explicit. Safest if we want another UI repair before rule changes.

Recommended next approval: Option 1, a narrow two-turn capture countdown, because it directly addresses “sneak capture” while staying small enough for one implementation branch.

## Not ready because

- Needs human choice among countdown, defense waves, control points, or clarity-only warning.
- Needs explicit decision on whether the story changes victory timing or only previews danger.
- Needs interaction rules for interruption: enemy presence, enemy capture, leaving the node, or end-turn ownership.
- Needs GDD/control wording before implementation so Codex does not invent strategic objective design.

## Candidate future acceptance ideas

These are not final acceptance criteria until the rule shape is approved:

- Objective state shows capture progress, owner/contester, and turns remaining.
- Capture cannot complete silently in one interaction unless explicitly designed as a special case.
- Opponent receives readable warning/counterplay opportunity.
- Defenses/guards are visible before commitment.
- Invalid or interrupted capture attempts explain why and do not partially mutate hidden state.

## Ambiguity Check

Status: FAIL.

Blockers:

- Objective capture rule shape is unapproved.
- Victory timing and interruption semantics are unapproved.
- Scope is not yet bounded enough for Codex implementation.

## Guarded prompt status

A guarded prompt exists at `production/sprints/codex-story-strat-objective-001.prompt.txt`, but it must self-block unless this story is promoted to `status: ready`, `approval: approved`, and Ambiguity Check `Status: PASS`.
