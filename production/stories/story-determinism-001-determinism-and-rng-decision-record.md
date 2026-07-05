---
title: STORY-DETERMINISM-001 Determinism and RNG Decision Record
type: story
status: review
phase: production
owner: shared
created: 2026-07-05
updated: 2026-07-05
source_lore: []
related:
  [
    production/epics/epic-vslice-mvp-015-post-audit-foundation-pivot-and-reconciliation,
    production/planning/post-audit-foundation-pivot-2026-07-03,
    docs/architecture/data-scenario-save-format-adr,
    docs/architecture/testing-strategy,
    docs/architecture/control-manifest,
    design/gdd/strategic-map,
    design/gdd/tactical-combat,
  ]
approval: approved
---

# STORY-DETERMINISM-001 Determinism and RNG Decision Record

## Status

REVIEW. Human delegation recorded 2026-07-05 after `STORY-GATE-001` merge request: "Verify and review, fix issues if any, then merge when done, then prepare next implementation packet." This promoted the next EPIC-015 child packet after the hollow-gate/source-truth reconciliation landed. Implementation branch `story/STORY-DETERMINISM-001-determinism-rng-adr` created the ADR and awaits PR review/merge.

## Story type

Architecture + Design Control.

## User/player/system value

As a designer and implementer, I need a clear determinism/RNG stance, so future data, tactical, dirty-information, AI, save/replay, and test work does not accidentally introduce randomness that breaks reproducibility or the intended uncertainty model.

## Source requirements

- Parent epic: `production/epics/epic-vslice-mvp-015-post-audit-foundation-pivot-and-reconciliation.md`.
- Pivot brief: `production/planning/post-audit-foundation-pivot-2026-07-03.md` lines on determinism and hollow control surfaces.
- Data/scenario/save ADR: `docs/architecture/data-scenario-save-format-adr.md` §Determinism note.
- Testing strategy: `docs/architecture/testing-strategy.md` domain/rules tests and deterministic random behavior coverage.
- Control manifest: `docs/architecture/control-manifest.md` implementation authority, data/tuning, testing, stop conditions.
- Strategic map GDD: `design/gdd/strategic-map.md` current hotseat MVP and strategic AI out-of-scope boundaries.
- Tactical combat GDD: `design/gdd/tactical-combat.md` MVP tactical rules and data-driven implementation guardrails.

## In scope

- Create `docs/architecture/determinism-and-rng-adr.md`.
- Decide and record the near-term policy: deterministic-by-default vs seeded RNG service.
- Define how uncertainty should be represented before full dirty-information systems exist.
- Define test/replay/save implications for future stories.
- Identify which future mechanics, if any, would require a seeded RNG service story.
- Update index/log/run-prompt discoverability.

## Out of scope

- Unity runtime code changes.
- Adding an RNG service.
- Changing combat damage, AI, tactical hit/crit rules, Intel, fog, save/load, scenario schema, or current deterministic gameplay.
- Broad GDD rewrites.
- Full dirty-information, false-intel, fog-of-war, or replay implementation.

## Acceptance criteria

- [x] `docs/architecture/determinism-and-rng-adr.md` exists and is indexed.
- [x] ADR chooses either deterministic-by-default or seeded RNG service for near-term MVP work.
- [x] ADR explains how dirty/source-tagged uncertainty differs from numeric randomness.
- [x] ADR states stop conditions for future stories that want random damage, AI randomness, procedural generation, hidden info rolls, or randomized rewards.
- [x] ADR records test/save/replay implications.
- [x] Follow-up stories are listed compactly if needed.

## Verification requirements

- `git diff --check`.
- Quartz build.

## Ambiguity Check

Status: PASS.

Approved assumptions / constraints:

- This is design/control repository work only.
- No Unity runtime implementation is authorized.
- Default recommendation is deterministic-by-default for MVP unless source review finds a stronger approved reason to require seeded RNG now.
- Future random mechanics must be explicit, seeded, testable, and story-approved.

## Runnable prompt

Runnable prompt: `production/sprints/codex-story-determinism-001.prompt.txt`. This is a design/control repo packet only; it must not modify Unity runtime code.

## Verdict

REVIEW. Determinism/RNG ADR prepared in the design/control repo only; PR review and merge remain.
