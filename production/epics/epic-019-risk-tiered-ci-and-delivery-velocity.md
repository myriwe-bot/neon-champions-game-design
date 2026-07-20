---
title: EPIC-019 Risk-Tiered CI and Delivery Velocity
type: epic
status: ready-candidate
phase: production
owner: shared
created: 2026-07-20
updated: 2026-07-20
approval: pending
related: [docs/architecture/testing-strategy, docs/architecture/ci-build-automation, production/stories/story-ci-risk-tiering-001-change-aware-unity-ci]
---

# EPIC-019 Risk-Tiered CI and Delivery Velocity

## Outcome

Keep strict, auditable AI-assisted delivery while removing redundant Unity work from documentation, pointer, evidence-lifecycle, and narrow implementation changes.

## Human direction

The owner explicitly challenged repeated full-suite runs, duplicate player windows, and screenshot regeneration as too slow and asked for a materially faster workflow. The approved direction at conversation level is risk-tiered verification; this packet still requires approval of the exact technical matrix before implementation.

## Capability sequence

1. `STORY-CI-RISK-TIERING-001` — READY-candidate / approval pending; change-aware jobs, one stable aggregate gate, no duplicate story-branch push run, docs-only fast path, scheduled full regression, and immutable-tree post-merge evidence.

## Boundaries

- Strict CI remains mandatory for production changes.
- No test deletion, assertion weakening, or coverage reduction.
- Unknown paths fail safe to the broad matrix.
- Human-only playability/visual gates remain human-owned.
- This epic changes CI routing and evidence policy, not gameplay or product behavior.

## Verdict

READY-candidate / approval pending. No runnable Codex packet yet.
