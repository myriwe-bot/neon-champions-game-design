---
title: STORY-CI-RISK-TIERING-001 Change-Aware Unity CI
status: ready-candidate
type: story
phase: production
owner: shared
created: 2026-07-20
updated: 2026-07-20
approval: pending
related: [production/epics/epic-019-risk-tiered-ci-and-delivery-velocity, docs/architecture/testing-strategy, docs/architecture/ci-build-automation]
---

# STORY-CI-RISK-TIERING-001 Change-Aware Unity CI

## Status

READY-candidate / approval pending. The owner has approved the need for faster risk-tiered verification, but the exact routing matrix below must be explicitly approved before this becomes runnable.

## Problem

The current single Unity workflow launches Compile/Standalone, EditMode, PlayMode, and Placeholder Validator for every PR and for both story-branch push and pull-request events. README-only pointer/evidence changes therefore trigger duplicate full runs, player windows, artifacts, and screenshots. A squash merge then repeats the same four jobs on an identical Git tree.

Observed waste on 2026-07-20:

- README-only pointer activation and evidence correction each triggered full exact-head and post-merge suites.
- PR #180 initially ran both push and pull-request matrices for one SHA.
- A final evidence-README-only correction would have repeated both matrices; the duplicate push event was intentionally cancelled while one exact-head PR matrix passed.
- PR #180 reviewed-head tree and merge tree were exactly identical: `13665466ccb9763cc589bed8fc201b9fc8f691d0`.

## Player/developer value

Implementation feedback arrives in minutes rather than tens of minutes, the self-hosted Windows runner is not occupied by irrelevant work, and strict checks remain aligned with actual blast radius.

## Proposed exact contract

### Event policy

- `pull_request`: run classification and the affected matrix once.
- Remove `story/**` and `spike/**` from automatic `push` triggers to eliminate duplicate same-SHA matrices.
- `push` to `main`: run a lightweight merge audit; do not blindly repeat the full reviewed matrix when merged tree identity is proven.
- `workflow_dispatch`: allow explicit full regression.
- `schedule`: run the full matrix nightly.

### Stable gate

- Add one always-present `CI Gate` job suitable for merge policy.
- It consumes classification plus optional job results and fails if any required affected job failed, was cancelled, or was incorrectly skipped.
- Unknown or unclassified Unity paths select the full matrix.

### Change classes

1. Docs/evidence lifecycle only
   - Examples: root/production Markdown, checked-in logs/XML/PNG evidence, pointer text.
   - Required: checkout, changed-file classification, whitespace/path hygiene, authority/pointer consistency where applicable.
   - Forbidden by default: Unity Editor, player build/launch, gameplay suites, screenshot regeneration.

2. CI/tooling only
   - Required: PowerShell/YAML syntax and focused script tests or dry-run fixtures.
   - Add representative Unity integration only when the changed script affects Unity invocation semantics.

3. Data/content/localization
   - Required: validator.
   - Add EditMode/PlayMode/build only when affected paths or story contract require them.

4. Domain/application logic
   - Required: focused tests during development and EditMode affected suite at immutable PR head.
   - Add other layers only for touched integration/data/build paths.

5. Scene/UI/presentation/integration
   - Required: PlayMode affected suite.
   - Add standalone build/launch for player-entry, scene boot, project settings, packages, build scripts, or story-required built-player behavior.

6. Broad/high-risk/unknown
   - Packages, serialization contracts, shared architecture, broad ProjectSettings, workflow classifier itself, or unclassified Unity path.
   - Required: full matrix.

### Post-merge policy

- Record PR reviewed head tree and merge tree.
- If equal, do not repeat full Unity suites; the lightweight main audit records identity and the exact reviewed CI URLs.
- If unequal or unprovable, fail closed and run/require the affected matrix.
- Human playtests remain separate and cannot be inferred from tree identity.

## In scope

- Split/refactor `.github/workflows/unity-foundation-ci.yml` as necessary.
- Add a repository-owned deterministic changed-path classifier and tests/fixtures.
- Add aggregate `CI Gate` semantics.
- Add nightly/manual full-regression entry points.
- Add lightweight post-merge tree/audit evidence.
- Update CI documentation and one evidence README.

## Out of scope

- Deleting tests, weakening assertions, changing gameplay/runtime/content, replacing GitHub Actions, changing Unity licensing, reducing required human gates, or silently treating skipped jobs as PASS.

## Acceptance criteria

- [ ] Docs/evidence-only fixture selects no Unity jobs and passes the stable gate.
- [ ] Domain fixture selects EditMode but not unrelated jobs.
- [ ] Data fixture selects validator.
- [ ] Scene/UI fixture selects PlayMode.
- [ ] Player-entry/ProjectSettings fixture selects standalone build/launch.
- [ ] Unknown-path fixture selects the full matrix.
- [ ] Story-branch push no longer duplicates pull-request CI.
- [ ] Nightly/manual full matrix remains available.
- [ ] Aggregate gate fails for any required failed/cancelled/skipped job.
- [ ] Equal-tree post-merge audit does not repeat Unity suites; unequal/unprovable tree fails closed.
- [ ] Existing test scripts remain callable and unchanged unless routing requires a narrow compatible adjustment.
- [ ] Evidence quantifies expected job/runtime reduction using recent PRs #178–#180.

## Testing policy

Focused script/classifier fixtures first. One workflow validation/dry run, then representative path-class PR evidence. Do not run the full Unity suite merely to validate docs-only classification; run a manual full matrix once before merge only because the classifier itself is high-risk CI infrastructure.

## Ambiguity check

PASS for candidate review. The proposed matrix, fallback, aggregate gate, event policy, scheduled regression, post-merge identity rule, and exclusions are explicit. Human approval is still required.

## Branch and PR

- Branch: `story/STORY-CI-RISK-TIERING-001-change-aware-unity-ci`
- PR title: `STORY-CI-RISK-TIERING-001 Change-aware Unity CI`

## Verdict

READY-candidate / approval pending. Guarded prompt only.
