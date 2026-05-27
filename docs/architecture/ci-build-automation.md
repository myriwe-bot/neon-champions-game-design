---
title: CI / Build Automation
type: adr
status: approved
phase: technical-setup
owner: shared
created: 2026-05-27
updated: 2026-05-27
source_lore: []
related: [docs/architecture/architecture, docs/architecture/control-manifest, docs/architecture/testing-strategy, docs/architecture/technical-decision-priorities, production/stories/story-template, production/epics/epic-template]
approval: approved
---

# CI / Build Automation

## Decision

Neon Champions adopts a strict CI policy.

CI is required immediately after the Unity project is created, including for spikes that live in the future production Unity repository. CI does not make spike code production-ready, but it does prove that the repository remains buildable, testable, and auditable from the start.

GitHub Actions is the default CI provider unless a later ADR approves a different provider.

No production PR may merge unless required automated checks pass or a human-approved exception is documented.

## Rationale

The project is designed for strict AI-assisted development. That requires an external, repeatable quality gate that is not dependent on an agent's claim, local editor state, or chat summary.

Strict CI from project creation protects against:

- broken Unity project setup;
- missing test runner configuration;
- agents disabling or bypassing checks;
- local-only success claims;
- silent validator failures;
- unreviewed prototype code drifting toward production.

## CI Timeline

### Stage A — Immediately After Unity Project Creation

Required before any spike PR is considered complete:

- Unity project opens/compiles in CI or equivalent Unity batchmode check.
- EditMode test runner is wired, even if only scaffold/smoke tests exist.
- Data/content/localization validator command is stubbed or implemented with explicit scope.
- CI result is linked in the PR or spike evidence.

Rule: spikes may remain prototype-only, but the repository must not become unverifiable.

### Stage B — Before First Production Story

Required:

- compile check;
- EditMode/domain tests;
- data/content/localization validators;
- evidence that required checks are merge-blocking;
- story template points to CI evidence.

### Stage C — Before Recurring Unity Integration Stories

Required:

- PlayMode/smoke tests for recurring scene, prefab, UI, and presentation/application integration paths;
- documented exceptions for any Unity integration behavior that cannot yet be automated;
- follow-up automation stories where manual evidence is temporary.

### Stage D — Before Vertical Slice

Required:

- CI verifies or produces a development build;
- PlayMode/smoke suite covers the main vertical-slice path;
- validators cover all MVP production data required by the slice.

### Stage E — Before Release

Required:

- CI produces release-candidate artifacts or verifies release-candidate build steps;
- regression tests pass;
- known issues, changelog, and release evidence are attached to release workflow.

## Initial Required Checks

After Unity project creation, the initial CI baseline should include:

1. Unity compile / batchmode project check.
2. EditMode test run.
3. Data/content/localization validator run, even if initially small.
4. PlayMode/smoke test run once the first PlayMode test exists.
5. Artifact upload for test logs where practical.

Exact Unity CLI commands, license setup, runner image, and caching strategy may be finalized when the Unity repository exists.

## Merge-Blocking Policy

For production PRs, these block merge unless a human-approved exception is documented:

- Unity compile failure;
- EditMode test failure;
- data/content/localization validator failure;
- required PlayMode/smoke failure;
- missing CI run link;
- missing story evidence;
- missing omissions section;
- missing explanation for skipped or deferred automation.

For spike/prototype PRs, these block completion unless explicitly accepted by a human:

- Unity project cannot compile/open in CI;
- CI is absent after project creation;
- spike boundaries are not declared;
- prototype code touches production paths without review;
- no evidence is linked.

## Exception Policy

Exceptions must be explicit. They must state:

- failed or missing check;
- reason;
- risk;
- owner;
- deadline or follow-up story;
- whether production merge is allowed or blocked.

Unacceptable exceptions:

- "CI was flaky" without an issue/follow-up;
- "manual tested" as a replacement for required automation;
- "agent could not run it" without environment diagnosis;
- disabling checks to pass a PR;
- weakening tests outside story scope.

## Agent Rules

Agents may not:

- create a Unity project without adding or preserving CI once the repository exists;
- mark a spike complete without CI evidence after project creation;
- mark a production story DONE without required CI evidence;
- disable, bypass, or weaken CI checks without approved scope;
- treat local-only success as merge-ready;
- hide failing checks behind manual evidence;
- remove test or validator coverage as incidental cleanup;
- merge or recommend merge with missing CI evidence unless a human-approved exception is recorded.

Agents must stop if:

- CI configuration is missing after Unity project creation;
- required checks cannot run;
- Unity license/runner setup blocks CI and no exception exists;
- a story requires merge-blocking checks but the repo has not configured them;
- checks fail for reasons outside the story scope.

## Evidence Requirements

Each PR or spike evidence package must include:

- CI run link;
- exact checks run;
- pass/fail summary;
- local test commands if local runs are used as supplemental evidence;
- validator output summary;
- PlayMode/smoke evidence when required;
- manual screenshots/video where required by the story type;
- omissions/stubs/mocks/assumptions/deferred work, or `No known omissions`.

## Approval Scope

This ADR approves:

- GitHub Actions as the default CI provider;
- CI required immediately after Unity project creation, including spike PRs;
- merge-blocking automated checks for production PRs;
- explicit exception policy;
- CI evidence as mandatory story/spike evidence once the Unity repo exists.

This ADR does not yet approve:

- exact Unity CLI commands;
- Unity license/activation mechanism;
- runner OS/image;
- caching strategy;
- final artifact retention policy;
- release build signing/package process.

Current verdict: APPROVED.
