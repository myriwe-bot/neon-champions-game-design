---
title: Control Manifest
type: adr
status: approved
phase: technical-setup
owner: shared
created: 2026-05-22
updated: 2026-07-05
source_lore: []
related:
  [
    docs/architecture/architecture,
    docs/architecture/unity-technical-scheme,
    docs/architecture/testing-strategy,
    docs/architecture/ci-build-automation,
    design/workflow,
    production/stories/story-template,
  ]
approval: approved
approval_scope: Technical setup, SPIKE-001 foundation work, and future implementation control gates.
---

# Control Manifest

This is the mandatory implementation rulebook for Codex and all coding agents.

It does not replace GDDs, ADRs, stories, tests, or human approval. It constrains how implementation happens.

Core rule: Codex is an implementer, not a designer or architect.

## 1. Implementation Authority

Agents may implement only when all of these are true:

- there is a READY story;
- the story links exact approved GDD sections;
- the story links exact approved architecture / ADR / control-manifest sections;
- scope is explicit;
- acceptance criteria are testable;
- evidence requirements are defined;
- ambiguity check is PASS;
- work happens through a traceable Git / GitHub branch and PR trail.

Agents may not:

- implement from chat memory;
- implement from worldbuilding directly;
- implement from epics;
- implement from draft or unapproved design docs;
- invent design, architecture, UX, balance, names, canon, assets, or content;
- reinterpret approved docs to make implementation easier.

## 2. Source Reading Order

Before coding, agents must read, in order:

1. READY story;
2. linked GDD sections;
3. linked ADR / architecture sections;
4. this control manifest;
5. linked UX / art / content docs;
6. linked worldbuilding or design-bridge docs, if lore-facing;
7. relevant existing code and tests.

If any required linked source is missing, draft, unapproved, or contradictory, stop and report.

## 3. Unity Project Rules

Production Unity implementation is blocked until the relevant technical scheme is approved.

The approved Unity rules must cover or explicitly mark N/A:

- Unity version;
- render pipeline;
- target platform;
- project and folder layout;
- assembly definitions;
- scene ownership;
- prefab ownership;
- ScriptableObject and data policy;
- input system;
- save/load boundary;
- package policy;
- testing strategy;
- CI/build automation;
- prototype vs production-code policy.

Until these are approved, only explicitly marked throwaway prototypes/spikes may touch Unity code.

## 4. Architecture Boundaries

Agents must use approved architecture patterns only.

Agents may not introduce, replace, or silently expand any of the following without ADR or architecture approval:

- global state;
- event buses;
- service locators;
- dependency injection containers;
- serialization systems;
- save/load systems;
- asset loading patterns;
- module or assembly boundaries;
- scene or prefab ownership rules;
- data-authoring pipeline.

Agents may not:

- refactor unrelated systems inside a feature story;
- create duplicate parallel systems;
- move system ownership across modules without approval;
- hide architecture changes inside gameplay work.

## 5. Data and Tuning

Rules:

- No hardcoded tunable gameplay values in production code unless explicitly approved.
- Use approved registries, config, data assets, or schemas for entities, stats, formulas, costs, rewards, and tuning knobs.
- Temporary data must be marked as placeholder and listed in PR omissions.
- Data schema changes require validation evidence.
- If the data-authoring path is undecided, stop instead of inventing it.
- A READY story may not claim registry coverage from a comment-only, empty, placeholder, or draft-pending registry file. It must either fill the registry/check in scope, mark the evidence N/A/deferred with a blocker, or link an approved follow-up story.

## 6. Testing and Verification

Every implementation story needs evidence. See `docs/architecture/testing-strategy.md`.

Minimum expectations:

- Production gameplay logic and bug fixes require TDD unless a human-approved exception is documented.
- Logic stories require automated EditMode/domain tests unless explicitly N/A.
- Data/config/content stories require automated validation tests or validation scripts.
- Unity scene, prefab, and UI stories require PlayMode/smoke evidence; automated PlayMode coverage is the target for recurring production integration paths.
- Manual Unity verification is supplemental, or temporary only when automation is not practical yet and the exception is documented.
- Visual/feel stories require screenshot, video, or a defined review protocol, plus PlayMode/smoke evidence when Unity wiring changes.
- CI failures must be fixed or explicitly human-accepted.
- After Unity project creation, CI evidence is required for spike completion and production PRs according to `docs/architecture/ci-build-automation.md`.
- "Could not test" is not acceptable without a documented blocker or human-approved exception.
- Passing a placeholder or always-green validator is not data/content/localization validation evidence. Stories and PRs must label that evidence as placeholder-only unless the check enforces the referenced registry or content rules.

Evidence must be linked or summarized in the PR.

## 7. Scope Control

Agents may not:

- add adjacent mechanics because they seem useful;
- promote full-vision features into MVP without gate approval;
- modify public-facing names, lore terms, faction framing, cultural references, or player-facing text unless the story explicitly allows it;
- alter balance, economy, AI behavior, UX, or content outside story scope;
- bundle unrelated cleanup with feature work.

If a better design or architecture idea appears during implementation, stop and propose it. Do not silently code it.

## 8. Documentation Rules

If implementation changes behavior, the correct document must be updated or the PR must explain why no document update is needed.

Agents must document:

- stubs;
- mocks;
- placeholders;
- assumptions;
- deferred work;
- known omissions;
- human-approved exceptions.

If source docs are stale, wrong, or contradictory, stop and request correction. Do not code around them silently.

## 9. Git / GitHub Rules

Production work must use Git / GitHub as the audit trail.

Rules:

- Work on a story-scoped branch.
- Commit only story-scoped changes.
- PR must link story ID, GDD section, ADR/control rule, and evidence.
- PR must include an omissions section.
- If there are no known omissions, PR must explicitly say: `No known omissions`.
- PR must link CI evidence once CI exists.
- No unrelated cleanup bundled into feature PRs.
- No direct push to main for production work.
- Do not hide generated or tool-created changes.

## 10. Stop Conditions

Stop and report instead of coding if:

- the story is not READY;
- the requested work is an epic, not an implementation story;
- ambiguity check is FAIL;
- linked GDD / ADR / control docs are missing;
- linked docs conflict;
- gameplay behavior is ambiguous;
- Unity architecture is undecided;
- implementation would require inventing mechanics, balance, UX, lore, names, assets, content, or architecture;
- work would exceed story scope;
- required tests or verification cannot be performed;
- CI is missing after Unity project creation;
- required CI checks fail or cannot run without a documented human-approved exception;
- Git working tree contains unrelated uncommitted changes;
- legal, IP, cultural, or asset-license risk appears;
- required asset provenance is unknown.

## 11. Manifest DONE Standard

This manifest is usable when:

- rules are short and operational;
- agents can follow them without interpretation;
- stop conditions are explicit;
- Unity unknowns are marked as blockers or placeholders;
- every production story can reference the manifest;
- the manifest supports, but does not replace, GDDs, ADRs, stories, and tests.

Current verdict: APPROVED as the technical-setup implementation control manifest.

Approval scope: this manifest approves implementation gates, source-reading rules, stop conditions, evidence requirements, and SPIKE-001 foundation constraints. It does not approve any production gameplay, mechanics, balance, content, save/load format, final data schema, or Unity implementation outside an approved spike or READY story.
