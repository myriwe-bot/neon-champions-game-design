---
title: Story Template
type: story
status: draft
phase: production
owner: shared
created: 2026-05-22
updated: 2026-07-05
source_lore: []
related:
  [
    design/workflow,
    docs/architecture/testing-strategy,
    docs/architecture/ci-build-automation,
    docs/architecture/control-manifest,
  ]
approval: pending
---

# Story: [STORY-ID] [Name]

## Status

Draft | NEEDS WORK | READY | BLOCKED | IN PROGRESS | REVIEW | DONE

## Story type

Logic | Integration | Visual/Feel | UI | Config/Data | Content | Tooling | Test | Playtest

## Parent epic

- Epic ID/path:

## User/player/system value

As a [player/designer/system], I want [capability], so that [value].

## Source requirements

Exact source references are required. Vague references such as "see tactical combat GDD" are not enough.

- GDD path + section/rule:
- ADR / architecture section / control-manifest rule:
- UX/content/art rule, if applicable:
- Worldbuilding or design-bridge source, if lore-facing:
- Parent epic:

## In scope

Concrete implementation tasks authorized by this story:

- ...

## Out of scope

Adjacent behavior not authorized by this story:

- ...

## Allowed stubs, mocks, placeholders, or temporary data

- None, or list explicitly.

## Dependencies

- Required prior stories:
- Required data/assets:
- Required architecture decisions:
- Required Unity/package setup:

## Acceptance criteria

Use observable/testable criteria. Prefer Given / When / Then where useful.

- [ ] Given [state], when [action], then [observable result].
- [ ] Given [state], when [invalid/edge action], then [observable result].

## Verification requirements

Use `docs/architecture/testing-strategy.md` to select required evidence by story type. Automated PlayMode coverage is the target for Unity integration; manual evidence must be supplemental or explicitly documented as a temporary exception.
Use `docs/architecture/ci-build-automation.md` for CI evidence and merge-blocking requirements once the Unity project exists.

- Unit tests:
- Unity edit-mode tests:
- Unity play-mode tests:
- Integration/data validation tests:
- Manual Unity scene/prefab checks:
- Screenshot/video evidence:
- Performance budget or N/A:
- CI evidence:
- Playtest evidence, if applicable: link `production/playtests/playtest-journal.md#...`, or state `N/A` with reason.
- TDD evidence required? Yes / No / N/A with reason:
- Automation deferred? No, or explain approved temporary exception:

If a verification type is N/A, explain why.

## Ambiguity Check

Status: PASS | FAIL

Open questions:

- None

Assumptions:

- None

Out of scope:

- ...

Allowed stubs/mocks:

- ...

Human-approved exceptions:

- None

If status is FAIL, this story is not READY.

## Branch / PR requirements

- Branch name:
- PR title:
- Required linked story ID:
- Required linked GDD/ADR/control docs:
- Required root/scoped AGENTS.md instructions:
- Required evidence summary:
- Required omissions section:

PR must explicitly list known omissions, stubs, mocks, assumptions, deferred work, or state `No known omissions`.

Closeout/playtest/readability/UX/visual-feel stories must preserve exact human complaints in quotes and link the journal entry used as evidence, or explicitly state why no playtest evidence applies.

## Story readiness gate

A story may be marked READY only when all items are true:

- [ ] Story has stable ID, title, type, status, and parent epic.
- [ ] User/player/system value is clear.
- [ ] Exact GDD source section is linked or explicitly N/A.
- [ ] Exact ADR/architecture/control-manifest source is linked or explicitly N/A.
- [ ] Relevant root/scoped AGENTS.md instructions are identified or explicitly N/A.
- [ ] UX/content/art/worldbuilding references are linked if relevant.
- [ ] In-scope work is concrete and bounded.
- [ ] Out-of-scope work is explicit.
- [ ] Stubs/mocks/placeholders are either disallowed or explicitly listed.
- [ ] Dependencies are listed and satisfied or marked blocking.
- [ ] Acceptance criteria are observable and testable.
- [ ] Verification requirements are defined according to `docs/architecture/testing-strategy.md`.
- [ ] Required automated tests/validators/PlayMode evidence are listed, or approved exceptions are documented.
- [ ] Ambiguity Check status is PASS.
- [ ] Branch / PR / CI traceability requirements are stated.
- [ ] Human approval has been given or delegated gate approval is recorded.

## DONE gate

A story may be marked DONE only when all items are true:

- [ ] Implementation matches approved story scope.
- [ ] Acceptance criteria pass.
- [ ] Required verification evidence exists.
- [ ] Required automated tests, validators, and PlayMode/smoke evidence pass, or human-approved exceptions are documented.
- [ ] No unauthorized design or architecture decisions were introduced.
- [ ] Omissions/stubs/mocks/deferred work are explicitly documented.
- [ ] PR/code review is complete.
- [ ] CI passes or human-approved exceptions are documented.
- [ ] Required docs were updated in the correct source-of-truth layer.

## Verdict

Draft | NEEDS WORK | READY | BLOCKED | DONE
