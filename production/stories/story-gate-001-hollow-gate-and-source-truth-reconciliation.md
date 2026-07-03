---
title: STORY-GATE-001 Hollow Gate and Source-Truth Reconciliation
type: story
status: ready-candidate
phase: production
owner: shared
created: 2026-07-03
updated: 2026-07-03
source_lore: []
related:
  [
    production/epics/epic-vslice-mvp-015-post-audit-foundation-pivot-and-reconciliation,
    production/planning/post-audit-foundation-pivot-2026-07-03,
    design/registry/entities,
    design/registry/formulas,
    design/registry/terms,
    design/world/faction-game-briefs,
    docs/architecture/control-manifest,
  ]
approval: pending
---

# STORY-GATE-001 Hollow Gate and Source-Truth Reconciliation

## Status

READY-candidate / approval pending.

## Story type

Process + Tooling + Documentation.

## User/player/system value

As a producer/reviewer, I want hollow control surfaces named and either filled, demoted, or deleted, so green gates and approved-looking templates do not imply false safety.

## In scope

- Create a reconciliation report listing hollow gates/templates/statuses found by the audit.
- Classify each as `fill`, `demote`, `delete`, or `needs owner decision`.
- Patch at least one low-risk source-truth drift item in the design repo.
- Add rule: no READY story may claim registry/validator coverage while the referenced file/check is a stub.

## Out of scope

- Broad rewriting of all GDDs.
- World-repo canon approval.
- Unity validator implementation, except as a future linked story.
- Resolving every open question in one pass.

## Acceptance criteria

- [ ] Reconciliation report exists and is indexed.
- [ ] Empty registry, faction brief template, placeholder validator, draft-source exceptions, and stale index/statuses are classified.
- [ ] At least one concrete drift fix is committed.
- [ ] Follow-up owner decisions are listed compactly.

## Verification requirements

- `git diff --check`.
- Quartz build.

## Ambiguity Check

Status: PASS.

## Verdict

READY-candidate / approval pending.
