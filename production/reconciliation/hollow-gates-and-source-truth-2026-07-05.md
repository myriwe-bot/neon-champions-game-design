---
title: Hollow Gates and Source-Truth Reconciliation - 2026-07-05
type: qa
status: approved
phase: production
owner: shared
created: 2026-07-05
updated: 2026-07-05
source_lore: []
related:
  [
    production/stories/story-gate-001-hollow-gate-and-source-truth-reconciliation,
    production/epics/epic-vslice-mvp-015-post-audit-foundation-pivot-and-reconciliation,
    production/planning/post-audit-foundation-pivot-2026-07-03,
    docs/architecture/control-manifest,
    production/stories/story-template,
    design/registry/entities,
    design/registry/formulas,
    design/registry/terms,
    design/world/faction-game-briefs,
  ]
approval: approved
---

# Hollow Gates and Source-Truth Reconciliation - 2026-07-05

## Purpose

This report records hollow or drift-prone design/control surfaces found during `STORY-GATE-001`. It does not approve new canon, mechanics, balance, validator code, Unity implementation, or broad GDD rewrites.

Classifications:

- `fill`: keep the surface, but make it real before future stories rely on it.
- `demote`: keep the surface only as a template, reference, or non-authoritative aid until approved.
- `delete`: remove the surface when it creates false confidence and has no clear owner.
- `needs owner decision`: do not resolve by agent cleanup; the owner must choose direction.

## Reconciliation Table

| Surface | Current evidence | Classification | Required next action |
| --- | --- | --- | --- |
| `design/registry/entities.yaml` | Comment-only stub: "Canonical game-facing entities. Draft pending." | `fill` | Create an approved registry schema/content story before any READY story claims entity-registry coverage. Until then it is not implementation authority. |
| `design/registry/formulas.yaml` | Comment-only stub: "Canonical formulas and tuning knobs. Draft pending." | `fill` | Fill with approved formula/tuning definitions plus validation, or keep stories from claiming formula-registry coverage. |
| `design/registry/terms.yaml` | Comment-only stub: "Canonical game-facing terminology. Draft pending." | `fill` | Fill with approved game-facing terminology and localization-key expectations before player-facing term authority depends on it. |
| `design/world/faction-game-briefs.md` | Draft/pending bridge template with no faction briefs. | `demote` | Treat as a non-authoritative template only. Do not use it to approve faction canon, campaign canon, names, rosters, or strategic identities. |
| Placeholder / always-green validator risk | Audit brief says the validator always passes; many older stories/prompts record "Placeholder Validator" as a passing gate. | `fill` | Replace with real data/content/localization checks in a future implementation/control story. Until then, passing placeholder-validator evidence proves only that the placeholder path ran. |
| Draft-source exceptions in implementation stories | Multiple stories use narrow human-approved exceptions for draft/pending GDD or planning sources. | `needs owner decision` | Owner should decide whether to promote cited sections, consolidate exceptions into approved design docs, or forbid new exceptions. Existing exceptions remain narrow and story-bound. |
| Stale index/status claims | `index.md` still listed several closed items as READY/IN PROGRESS; `STORY-QA-014` body still said READY while frontmatter and EPIC-013 said DONE. | `fill` | Patched in this story: index status lines now match current source files, and `STORY-QA-014` body/verdict now records DONE / merged. |

## Gate Rule Added

`docs/architecture/control-manifest.md` and `production/stories/story-template.md` now state that a READY story may not claim registry or validator coverage while the referenced registry/check is a stub, placeholder, comment-only file, or always-green check. Such coverage must be marked N/A/deferred/blocking unless the story fills the registry/check or links an approved follow-up blocker.

## Drift Fix Applied

Low-risk drift fix:

- Updated stale `index.md` status lines for EPIC-012, `STORY-INTEL-DIRTY-003`, EPIC-013, `STORY-QA-014`, EPIC-014, and `STORY-TAC-ROLE-001`.
- Updated the body status and verdict in `production/stories/story-qa-014-epic-013-playtest-and-closeout-review.md` to match its `status: done` frontmatter and EPIC-013 closeout evidence.

## Follow-Up Owner Decisions

- Decide whether the registry YAML files should be filled as approved data registries or deleted/demoted until a concrete data-authoring lane needs them.
- Decide whether `design/world/faction-game-briefs.md` should become a real approved design bridge, remain a template, or move out of production-facing source authority.
- Decide whether historical draft-source exceptions should be consolidated into approved GDD sections.
- Decide the future Unity story that replaces the placeholder validator with real enforceable checks.

## Unity Runtime Scope

No Unity runtime, tests, scenes, prefabs, assets, packages, or ProjectSettings changes are authorized or made by this report.
