---
title: STORY-QA-005 PlayMode Evidence Artifact Hygiene
type: story
status: ready
phase: production
owner: shared
created: 2026-06-12
updated: 2026-06-13
source_lore: []
related:
  [
    docs/architecture/testing-strategy,
    docs/architecture/ci-build-automation,
    production/stories/story-ux-001-strategic-map-readability-action-clarity-pass,
  ]
approval: approved
---

# STORY-QA-005 PlayMode Evidence Artifact Hygiene

## Status

READY / approved. Human approved implementation on 2026-06-13 for PlayMode evidence artifact hygiene only: no gameplay/UI changes, no committed evidence deletion, preserve local evidence override, reduce stale CI evidence paths and artifact quota pressure.

## Why this story exists

During `STORY-UX-001` review, Unity CI successfully proved the exact-head branch and post-merge `main`, but two evidence-pipeline weaknesses became visible:

1. `ci/RunPlayModeTests.ps1` still writes generated PlayMode evidence to the historical `production/evidence/STORY-QA-003/generated` directory.
2. GitHub artifact upload hit the repository/account artifact storage quota, making generated PlayMode evidence unavailable from Actions even when tests run.

This does not add gameplay value, but it protects the story train: future review should not depend on stale evidence paths or quota-fragile artifact behavior.

## Player/design value

Indirect. It makes the vertical-slice review loop more reliable so gameplay stories can keep shipping with trustworthy CI/evidence.

## Implementation scope

One narrow CI/test-evidence hygiene pass:

- Stop hard-coding `STORY-QA-003` as the only PlayMode evidence output location.
- Use a neutral CI evidence path under `artifacts/playmode/evidence` by default.
- Preserve explicit `-neonChampionsEvidenceDir` / `NEON_CHAMPIONS_EVIDENCE_DIR` override behavior for local story evidence generation.
- Keep checked-in story evidence directories intact; do not delete historical evidence.
- Reduce GitHub artifact pressure:
  - upload PlayMode logs/results and generated evidence only from `artifacts/playmode`, or
  - split/log-only if safer,
  - set short artifact retention if supported.
- Keep the PlayMode failure-summary improvement introduced during `STORY-UX-001` review.
- Add or update lightweight script/validator checks that prove the CI PlayMode evidence path is no longer stale/hard-coded to `STORY-QA-003`.
- Update docs/readmes that tell reviewers where generated CI evidence lives.

## Out of scope

- No gameplay changes.
- No UI changes.
- No story/evidence PNG regeneration unless needed to verify path behavior.
- No deletion of committed evidence.
- No broad CI rewrite.
- No runner machine cleanup, billing changes, or manual GitHub storage administration.
- No new Unity test content beyond CI/evidence-path verification.

## Acceptance criteria

- `ci/RunPlayModeTests.ps1` no longer hard-codes `production/evidence/STORY-QA-003/generated` as the default evidence directory.
- PlayMode test results/logs remain uploaded or printed in a useful form even if evidence upload is skipped or quota-limited.
- Workflow artifact upload path is not stale and uses short retention where appropriate.
- Existing Unity Foundation CI jobs still run:
  - compile
  - EditMode
  - Placeholder Validator
  - PlayMode Smoke Tests
- Existing PlayMode evidence capture override still works for local story PNG generation.
- No existing checked-in evidence is removed.
- `git diff --check` passes.
- PR exact-head CI passes.

## Suggested implementation branch

`story/STORY-QA-005-playmode-evidence-artifact-hygiene`

## Suggested PR title

`STORY-QA-005 PlayMode evidence artifact hygiene`

## Ambiguity check

Status: PASS.

Human-approved implementation constraints:

- PlayMode evidence artifact hygiene only.
- No gameplay changes.
- No UI changes.
- No committed evidence deletion.
- Preserve local evidence override behavior.
- Reduce stale CI evidence paths and artifact quota pressure.
