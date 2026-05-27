---
title: Multi-Agent Operating Model
type: agent-instructions
status: approved
phase: technical-setup
owner: shared
created: 2026-05-27
updated: 2026-05-27
source_lore: []
related: [docs/architecture/codex-agent-instructions, docs/architecture/control-manifest, docs/architecture/testing-strategy, docs/architecture/ci-build-automation, production/checklists/codex-pr-review-checklist]
approval: approved
---

# Multi-Agent Operating Model

## Decision

Neon Champions may use many agents, but not as an uncoordinated swarm.

The approved model is role-based, gate-driven, branch/worktree-isolated, and human-controlled. Agents may accelerate drafting, implementation, QA, and review, but human approval remains required for creative direction, production scope, exceptions, and merges.

## Core Principle

Many agents are useful only when each agent has:

- a bounded role;
- a single clear task;
- isolated files/branch/worktree;
- explicit source documents;
- a defined gate;
- required evidence;
- stop conditions.

More agents without isolation and gates create conflicts, generic design, and unverifiable work.

## Roles

### Human Owner

Authority:

- creative direction;
- design approval;
- scope approval;
- architecture approval;
- risk acceptance;
- exception approval;
- final merge/release approval.

Human decisions should be recorded in approved docs, not left only in chat.

### Design Agent

Allowed:

- draft GDD sections;
- propose options and trade-offs;
- map systems;
- detect contradictions;
- prepare epics/stories from approved design.

Not allowed:

- approve its own design;
- invent canon/content as production truth;
- turn worldbuilding directly into implementation.

### Architecture Agent

Allowed:

- draft ADRs;
- propose technical options;
- inspect risks;
- define test/CI/data/tooling strategies;
- review whether implementation work has enough technical authority.

Not allowed:

- silently decide open architecture questions;
- change approved technical direction without human gate.

### Coordinator Agent

Allowed:

- decompose approved work into tasks;
- reserve files/assets;
- create task prompts;
- route work to implementation/review/QA agents;
- maintain status and evidence links.

Not allowed:

- assign implementation without READY story or approved spike;
- allow parallel agents to touch the same high-conflict assets.

### Implementation Agent / Codex

Allowed:

- implement approved spike scope;
- implement READY story scope;
- write tests/validators/evidence required by the task;
- propose blockers or follow-up stories.

Not allowed:

- implement from chat memory;
- implement epics directly;
- invent design, balance, UX, lore, content, architecture, package choices, save/load, localization, or data schemas;
- weaken tests/CI/gates to pass.

### QA / Verification Agent

Allowed:

- run tests and validators;
- inspect CI evidence;
- check story DONE gate;
- verify screenshots/video/manual evidence exists;
- identify missing evidence.

Not allowed:

- accept missing evidence without human-approved exception;
- redefine acceptance criteria after implementation.

### Review Agent

Allowed:

- review PRs against approved story/spike, GDD, ADR, control manifest, and AGENTS.md scope;
- detect unauthorized changes;
- flag bugs, missing tests, scope creep, Unity asset risks, and omissions.

Not allowed:

- substitute for human final approval;
- invent new creative direction during review;
- accept changes because the implementer says they are fine.

## Handoff Chain

Canonical chain:

```text
Worldbuilding source
-> design bridge / lore import
-> GDD
-> ADR / control rule
-> epic
-> READY story or approved spike
-> implementation branch/worktree
-> tests / validators / CI / evidence
-> review
-> human merge / DONE acceptance
```

A downstream agent must stop if an upstream artifact is missing, draft, contradictory, or too vague for the requested task.

## Parallel Agent Rules

Parallelism is allowed only when conflict risk is controlled.

Rules:

- One implementation agent = one approved task = one branch/worktree.
- Do not run multiple implementation agents in the same working tree.
- Do not run parallel agents on the same Unity scene, prefab, ScriptableObject database, animation controller, package file, ProjectSettings area, or generated asset path.
- Prefer parallel work across independent boundaries:
  - domain logic vs docs;
  - validator tooling vs UI mockups;
  - independent GDD review vs ADR review;
  - separate stories touching separate assemblies/assets.
- Use reviewer agents after implementation, not as a replacement for tests/CI.

## Worktree / Branch Policy

For implementation work:

- branch/worktree names should include story or spike ID;
- branches should be small and scoped;
- main is protected from direct production pushes;
- unrelated cleanup is not bundled;
- high-conflict Unity assets must be reserved before work begins.

Recommended branch examples:

```text
spike/spike-001-unity-ci-foundation
story/nc-123-movement-point-spending
review/pr-123-spec-check
```

## Gate Types

### Pre-flight Gate

Before implementation:

- story is READY or spike is approved;
- source references are exact;
- ambiguity check passes;
- required evidence is defined;
- affected files/assets are identified;
- parallel conflicts are checked.

Failure behavior: revise docs/story/spike, do not code.

### Plan Gate

For risky or broad tasks:

- agent researches code/assets;
- agent lists intended files/scenes/prefabs/data to touch;
- agent lists tests/evidence to run;
- human or coordinator approves the plan.

Failure behavior: revise plan or split task.

### Implementation Gate

During implementation:

- agent stays inside scope;
- TDD is followed for production logic/bugs;
- stop conditions are honored;
- no unapproved architecture/design decisions are introduced.

Failure behavior: stop and report blocker.

### Verification Gate

Before PR/DONE:

- required tests pass;
- validators pass;
- CI passes once available;
- PlayMode/smoke/manual evidence exists where required;
- omissions are disclosed.

Failure behavior: fix, document exception, or block.

### Review Gate

Before human merge:

- spec compliance review passes;
- code/asset quality review passes;
- scope creep scan passes;
- documentation/evidence review passes.

Failure behavior: request changes and re-review.

## Reviewer Model

Use at least two review lenses for important implementation PRs:

1. Spec compliance reviewer:
   - checks whether the implementation exactly matches approved story/spike scope;
   - flags missing or extra behavior.

2. Quality/safety reviewer:
   - checks correctness, maintainability, tests, Unity asset integrity, CI, omissions, and stop-condition risks.

For high-risk Unity asset work, add a Unity asset reviewer focused on scenes/prefabs/meta/settings/package changes.

## Evidence Package Standard

Every implementation PR/spike completion must report:

- story/spike ID;
- source docs read;
- files changed;
- Unity assets/settings/packages changed;
- tests/checks/validators run;
- CI link once CI exists;
- manual evidence paths where applicable;
- omissions/stubs/mocks/assumptions/deferred work or `No known omissions`;
- stop-condition risks or explicit `No known stop-condition risks`.

## Conflict Resolution

Priority order:

1. system/developer/user instruction in the active session;
2. approved project docs;
3. root/scoped `AGENTS.md`;
4. current story/spike;
5. implementation findings;
6. chat memory / agent memory.

If approved docs and implementation reality conflict, treat divergence as a defect or blocker until reviewed. Do not silently update code to match a private assumption.

## When to Use Many Agents

Good uses:

- independent research tasks;
- separate ADR option analysis;
- spec review vs quality review;
- parallel implementation of independent stories in separate worktrees;
- QA/evidence verification after implementation.

Bad uses:

- multiple agents editing one Unity scene;
- multiple agents changing the same architecture boundary;
- agents generating creative direction independently;
- parallel implementation before GDD/ADR/story approval;
- using reviewers to compensate for missing tests.

## Current Verdict

APPROVED.
