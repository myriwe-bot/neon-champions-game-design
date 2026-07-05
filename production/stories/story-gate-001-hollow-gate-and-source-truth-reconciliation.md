---
title: STORY-GATE-001 Hollow Gate and Source-Truth Reconciliation
type: story
status: ready
phase: production
owner: shared
created: 2026-07-03
updated: 2026-07-05
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
approval: approved
---

# STORY-GATE-001 Hollow Gate and Source-Truth Reconciliation

## Status

READY / approved. Human approval recorded 2026-07-05 via instruction after `STORY-PLAYTEST-001` merge: "Verify and review, fix issues if any, then merge when done, then prepare next implementation packet." This promotes the next EPIC-015 child packet after the playtest journal/gate hook landed.

## Story type

Process + Tooling + Documentation.

## User/player/system value

As a producer/reviewer, I want hollow control surfaces named and either filled, demoted, or deleted, so green gates and approved-looking templates do not imply false safety.

## In scope

- Create `production/reconciliation/hollow-gates-and-source-truth-2026-07-05.md` listing hollow gates/templates/statuses found by the audit.
- Classify each as `fill`, `demote`, `delete`, or `needs owner decision`.
- Patch at least one low-risk source-truth drift item in the design repo.
- Add rule: no READY story may claim registry/validator coverage while the referenced file/check is a stub.
- Update index/log/run-prompt discoverability.

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

Approved assumptions / constraints:

- This is design/control repository work only.
- Draft/pending/empty sources such as `design/world/faction-game-briefs.md` and the registry YAML stubs are in scope as hollow surfaces to classify; Codex must not treat them as approved content authority.
- At least one low-risk correction is required, but broad GDD rewrites, world canon approvals, and Unity validator implementation remain out of scope.

## Runnable prompt

Runnable prompt: `production/sprints/codex-story-gate-001.prompt.txt`. This is a design/control repo packet only; it must not modify Unity runtime code.

## Verdict

READY / approved. Prepare the hollow-gate/source-truth reconciliation report and one or more low-risk design-control drift fixes only.
