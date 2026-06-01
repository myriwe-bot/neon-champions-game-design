---
title: Merge to Main Gate
type: adr
status: in-review
phase: technical-setup
owner: shared
created: 2026-06-01
updated: 2026-06-01
source_lore: []
related: [docs/architecture/control-manifest, docs/architecture/testing-strategy, docs/architecture/ci-build-automation, docs/architecture/multi-agent-operating-model, production/checklists/codex-pr-review-checklist]
approval: pending
---

# Merge to Main Gate

## Status

In review / pending human approval.

This workflow defines the required gate sequence before any Unity implementation branch merges into `main`. It is intended to become binding after human approval.

## Decision

No implementation branch may merge into `main` unless it passes the merge-to-main gate.

The gate is fail-closed: if required evidence is missing, contradictory, or unverifiable, the merge is blocked until fixed or explicitly accepted by the human with a documented exception.

Default merge method: squash merge through a pull request. Direct pushes to `main` are not allowed for production work.

## Applies to

- Unity implementation repository PRs.
- Spike PRs after Unity project creation.
- Production story PRs.
- Follow-up fix PRs that affect implementation, tests, CI, project settings, scenes, prefabs, packages, or generated Unity metadata.

Documentation-only changes in the game-design repo may use normal doc review, but any doc change that changes implementation authority, gates, testing, CI, or merge policy should use this gate before being treated as binding.

## Roles

- Implementer: writes the code and evidence package.
- Gate runner: verifies the merge gate and records verdict. May be Hermes or another agent.
- Independent reviewer: reviews the PR without relying on implementer claims.
- Human: approves exceptions, resolves design/architecture ambiguity, and may require additional review.

A single agent may not both implement and be the only reviewer for a production merge. At minimum, the gate runner must perform an independent review pass after implementation.

## Gate sequence

### Gate 0 — Branch and PR hygiene

Required:

- [ ] Work is on a story/spike-scoped branch.
- [ ] PR targets `main` unless explicitly using an approved stacked-branch workflow.
- [ ] Branch is up to date with target branch or merge/rebase conflict status is known.
- [ ] PR title includes the story/spike ID when applicable.
- [ ] PR body links the story/spike and source docs.
- [ ] PR body includes omissions/stubs/mocks/assumptions/deferred work, or states `No known omissions`.
- [ ] No unrelated files are changed.
- [ ] No generated, package, ProjectSettings, scene, prefab, or `.meta` changes are present unless in scope and explained.

Blocks merge if:

- direct push to `main` is proposed;
- PR has no story/spike authority;
- branch includes unrelated changes;
- PR body lacks required traceability or omissions section.

### Gate 1 — Source authority

Required for production stories:

- [ ] Story status is READY.
- [ ] Story approval is recorded.
- [ ] Story has parent epic or explicit N/A.
- [ ] Story links exact approved GDD sections.
- [ ] Story links approved architecture/ADR/control-manifest sections.
- [ ] Acceptance criteria and verification requirements are present.
- [ ] Ambiguity check is PASS.

Required for spikes:

- [ ] Spike status is approved or explicitly authorized.
- [ ] Spike scope and non-production boundaries are stated.
- [ ] Required spike evidence is defined.

Blocks merge if:

- implementation is from chat memory, epic-only scope, draft docs, or unapproved lore;
- any required source doc is missing, draft, contradictory, or ambiguous;
- implementation required a new design/architecture/content decision not recorded in the right source layer.

### Gate 2 — Scope compliance

Required:

- [ ] Changed files match the story/spike in-scope section.
- [ ] Out-of-scope exclusions were not implemented.
- [ ] No full-vision features leaked into MVP.
- [ ] No new player-facing names, lore, content, UX, packages, save/load systems, data-authoring pipelines, service locators, global state, or event buses were introduced unless explicitly authorized.
- [ ] Temporary data/placeholders are allowed by the story and listed in omissions.

Blocks merge if:

- implementation expands scope because it was convenient;
- architecture or data pipeline decisions are hidden inside feature work;
- placeholder content becomes player-facing without approval.

### Gate 3 — Architecture and Unity asset safety

Required:

- [ ] Assembly dependencies respect the approved direction.
- [ ] Domain code has no `UnityEngine` dependency unless explicitly approved.
- [ ] Gameplay rules are not owned by MonoBehaviours, scenes, prefabs, or ScriptableObjects.
- [ ] Runtime state remains serializable-friendly where required.
- [ ] ProjectSettings, Packages, scenes, prefabs, ScriptableObjects, animation controllers, generated files, and `.meta` changes are listed and justified.
- [ ] No package or Unity version changes unless approved.

Suggested local checks:

```bash
git diff --name-only main...HEAD
git diff main...HEAD --stat
git diff main...HEAD -- Assets/ ProjectSettings/ Packages/
```

Blocks merge if:

- Unity asset/settings/package changes are unexplained or out of scope;
- domain/application/presentation/data ownership is violated;
- required `.meta` files are missing or casually deleted.

### Gate 4 — TDD and evidence integrity

Required for production logic and bug fixes:

- [ ] PR includes RED/GREEN evidence or states a human-approved TDD exception.
- [ ] New behavior has automated tests at the layer required by the story.
- [ ] Acceptance criteria are mapped to tests/evidence.
- [ ] Tests cover invalid/error cases required by the story, not only happy path.
- [ ] No tests were weakened, deleted, or skipped outside scope.

Blocks merge if:

- production logic was added without tests;
- tests were written only after implementation and no exception is recorded;
- required acceptance criteria lack evidence;
- test failures are handwaved.

### Gate 5 — Local verification

Required:

- [ ] Exact local commands and results are recorded in the PR or evidence file.
- [ ] Relevant Unity compile/test/validator commands were run locally when available.
- [ ] `git diff --check` passes.
- [ ] Any local command that cannot run is explained with environment diagnosis, not just "could not test".

Minimum expected commands for Unity implementation PRs, adjusted to the repo's actual scripts:

```bash
git diff --check
# Unity compile / batchmode check, if configured
# Unity EditMode tests
# Unity PlayMode/smoke tests when required
# data/content/localization validator when required
```

Blocks merge if:

- required local verification is absent and CI cannot substitute for it;
- commands fail for reasons introduced by the PR;
- the inability to run checks is unexplained.

### Gate 6 — CI and branch protection

Required:

- [ ] CI run link is present.
- [ ] Required checks are green on the PR head commit.
- [ ] Required checks are merge-blocking for production PRs, or a human-approved exception is recorded.
- [ ] CI includes compile, EditMode tests, validators, and required PlayMode/smoke checks according to the story type and current CI stage.
- [ ] No workflow was weakened, disabled, or bypassed to make the PR pass.

Blocks merge if:

- CI is missing after Unity project creation;
- required checks are red, cancelled, skipped, stale, or not run on the final commit;
- CI evidence is local-only for a production merge;
- branch protection/merge-blocking checks are absent when required and no exception exists.

### Gate 7 — Independent review

Required:

- [ ] Independent reviewer reads PR description, story/spike, changed files, and diff.
- [ ] Reviewer checks correctness, scope, architecture boundaries, tests, security/secrets, and Unity asset safety.
- [ ] Critical or warning-level findings are fixed or escalated to the human.
- [ ] Reviewer verdict is recorded: APPROVE, COMMENT, REQUEST CHANGES, or BLOCKED.

Minimum review checklist:

- Correctness: code does what story requires; edge cases handled.
- Scope: no unauthorized adjacent behavior.
- Architecture: dependencies and ownership are correct.
- Security: no secrets, unsafe shell/eval/deserialization, or data exfiltration risk.
- Testing: required evidence exists and is meaningful.
- Unity safety: assets/settings/packages/meta changes are justified.

Blocks merge if:

- reviewer requests changes;
- reviewer cannot verify scope/evidence;
- review is performed only by the original implementer.

### Gate 8 — Documentation and evidence sync

Required:

- [ ] Implementation evidence is stored in the Unity repo/PR unless an approved policy says otherwise.
- [ ] Any source-of-truth doc updates are made in the correct repo/layer.
- [ ] If implementation exposed missing design/architecture requirements, the story/GDD/ADR is updated or a follow-up is created before merge.
- [ ] Story DONE gate items are checked or explicitly left open with reason.
- [ ] Epic progress is updated only after child story status/evidence supports it.

Blocks merge if:

- docs and implementation conflict;
- story is marked DONE without required evidence;
- omissions are hidden.

### Gate 9 — Final merge decision

Required:

- [ ] Gates 0-8 are PASS, or every exception is human-approved and documented.
- [ ] PR head commit is the same commit that passed CI/review.
- [ ] PR has no unresolved review threads or requested changes.
- [ ] Merge method is squash unless human explicitly chooses another method.
- [ ] Branch is deleted after merge unless retained for a documented reason.
- [ ] Local `main` is updated after merge.

Suggested commands with GitHub CLI:

```bash
gh pr view <PR> --json mergeStateStatus,reviewDecision,statusCheckRollup,headRefOid,isDraft
gh pr checks <PR>
gh pr merge <PR> --squash --delete-branch
```

Without GitHub CLI, use GitHub REST/API or the web UI, but record the same evidence.

Blocks merge if:

- PR is draft;
- review decision is CHANGES_REQUESTED;
- required checks are not green;
- the final commit differs from reviewed/green commit;
- any gate is unresolved.

## Exception policy

Only the human may approve exceptions to merge-blocking gates.

Each exception must record:

- gate ID;
- failed or missing requirement;
- reason;
- risk;
- owner;
- deadline or follow-up story/issue;
- whether merge is allowed despite the exception.

Unacceptable exceptions:

- "CI flaky" without run evidence and follow-up.
- "Manual tested" replacing required automation.
- "Agent could not run it" without environment diagnosis.
- Disabling tests/checks to pass.
- Merging undocumented scope creep.
- Hiding design/architecture decisions inside implementation.

## Gate verdict format

Use this format in PR comments or evidence files:

```text
Merge-to-main gate verdict: PASS | BLOCKED | PASS WITH HUMAN-APPROVED EXCEPTION

PR:
Branch:
Head commit:
Story/spike:
Reviewer:
CI run:

Gates:
- Gate 0 Branch and PR hygiene: PASS/BLOCKED — evidence
- Gate 1 Source authority: PASS/BLOCKED — evidence
- Gate 2 Scope compliance: PASS/BLOCKED — evidence
- Gate 3 Architecture and Unity asset safety: PASS/BLOCKED — evidence
- Gate 4 TDD and evidence integrity: PASS/BLOCKED — evidence
- Gate 5 Local verification: PASS/BLOCKED — evidence
- Gate 6 CI and branch protection: PASS/BLOCKED — evidence
- Gate 7 Independent review: PASS/BLOCKED — evidence
- Gate 8 Documentation and evidence sync: PASS/BLOCKED — evidence
- Gate 9 Final merge decision: PASS/BLOCKED — evidence

Exceptions:
- None | documented exception list

Omissions/stubs/mocks/assumptions/deferred work:
- None | list

Final decision:
- Merge allowed | Merge blocked
```

## Minimal merge rule summary

A PR can merge only when all of this is true:

1. It has approved authority: READY story or approved spike.
2. It stays within scope.
3. It obeys architecture and Unity asset rules.
4. Required TDD/tests/evidence exist.
5. Local verification and CI pass on the final commit.
6. Independent review approves it.
7. Omissions and exceptions are explicit.
8. Human approval exists for any exception.
9. Merge happens via PR, preferably squash merge.

Current verdict: IN REVIEW.
