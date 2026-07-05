---
title: STORY-GATE-001 Hollow Gate and Source-Truth Reconciliation
type: story
status: done
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

DONE / merged. Game-design PR #2 merged 2026-07-05 as `a63aeb36832ecead9ef7eb2309d07fddab1169c8`; post-merge publish CI passed at https://github.com/myriwe-bot/neon-champions-game-design/actions/runs/28741706267. Human approval recorded 2026-07-05 via instruction after `STORY-PLAYTEST-001` merge: "Verify and review, fix issues if any, then merge when done, then prepare next implementation packet."

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

- [x] Reconciliation report exists and is indexed.
- [x] Empty registry, faction brief template, placeholder validator, draft-source exceptions, and stale index/statuses are classified.
- [x] At least one concrete drift fix is committed.
- [x] Follow-up owner decisions are listed compactly.

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

## Implementation notes

- Reconciliation report: `production/reconciliation/hollow-gates-and-source-truth-2026-07-05.md`.
- Low-risk drift fix: stale `index.md` status lines and `STORY-QA-014` body/verdict corrected to match DONE / merged evidence.
- Rule hook: `docs/architecture/control-manifest.md` and `production/stories/story-template.md` now block registry/validator coverage claims from stub or always-green checks.
- Unity runtime scope: N/A; this packet is design/control only.

## DONE evidence

- Game-design PR: https://github.com/myriwe-bot/neon-champions-game-design/pull/2
- Merge commit: `a63aeb36832ecead9ef7eb2309d07fddab1169c8`
- Post-merge publish CI: https://github.com/myriwe-bot/neon-champions-game-design/actions/runs/28741706267
- Local verification before merge: `git diff --check`; `git diff origin/main...HEAD --check`; `npm run build` parsed 176 Markdown files and emitted 487 files.

## Verdict

DONE / merged. Hollow-gate/source-truth reconciliation report and registry/validator guard hooks are available in the design/control repo.
