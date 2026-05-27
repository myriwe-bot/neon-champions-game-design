---
title: Game Design Workflow
type: concept
status: draft
phase: concept
owner: shared
created: 2026-05-22
updated: 2026-05-27
source_lore: []
related: [design/game-design-principles, production/gates/review-mode]
approval: pending
---

# Game Design Workflow

This project follows a Claude Code Game Studios-style flow adapted for strict human-led design and agent-safe implementation.

## Core Operating Rule

Neon Champions uses a human-led, agent-assisted workflow.

Humans own:
- creative direction;
- game design decisions;
- final approval;
- scope calls.

Documents own:
- approved lore imports;
- GDD rules;
- Unity architecture;
- production story requirements.

Agents and Codex may:
- research;
- propose options;
- draft docs;
- review gates;
- implement approved stories;
- verify with evidence.

Agents and Codex may not:
- implement from chat memory;
- turn unapproved lore into gameplay rules;
- invent missing mechanics during coding;
- silently choose Unity architecture;
- implement vague epics directly.

Hard rule: no production implementation until there is a READY story that traces to approved GDDs and approved technical rules.

## Source-of-Truth Model

The project has four authoritative source-of-truth layers.

### 1. Worldbuilding Truth

Lives in the Neon Champions world vault.

Contains exploratory and approved setting material: history, factions, locations, world rules, mysteries, technologies, and lore.

Worldbuilding may contain hard canon, soft canon, in-world belief, rumor, raw brainstorms, references, rejected ideas, and contradictions.

Worldbuilding does not automatically authorize gameplay rules or implementation.

### 2. Game Design Truth

Lives in this game-design repo under `design/`.

Contains approved game-facing artifacts: concept, pillars, MVP scope, systems index, system GDDs, UX specs, balance rules, and design bridges.

Game design translates worldbuilding into playable rules.

Production mechanics must trace to this layer.

### 3. Technical Truth

Lives under `docs/architecture/`.

Contains Unity architecture, ADRs, data model, testing strategy, folder structure, Codex operating rules, performance budgets, CI/build rules, and the control manifest.

Implementation must obey this layer.

Codex and other agents may not invent architecture during feature work.

### 4. Production Truth

Lives under `production/`.

Contains epics, READY stories, sprint plans, QA reports, playtest reports, verification evidence, and gate decisions.

Epics organize work.

READY stories authorize implementation.

## Support and Evidence Categories

These categories support decisions and verification, but they do not override approved source-of-truth documents.

### 5. Prototype / Spike Evidence

Lives under `prototypes/` or `production/spikes/`.

A prototype answers a design or technical question. It does not authorize production implementation.

Prototype code is throwaway unless explicitly reviewed and promoted.

### 6. Asset / Content Pipeline Rules

Lives under `design/art/`, `design/ux/`, `docs/architecture/content-pipeline.md`, and later Unity asset documentation.

Defines placeholder policy, licensing, naming, import settings, asset ownership, accessibility constraints, and content safety rules.

### 7. References / Legal / Cultural Constraints

Lives under `design/references/`, world-vault raw references, or dedicated policy docs.

Includes inspirations, genre research, HoMM / Olden Era analysis, real-world references, cultural naming notes, legal/IP boundaries, and sensitivity constraints.

Reference material is not canon or design until promoted through approval.

### 8. Chat / Memory / Agent Output

Chat, memory, and agent summaries are not source of truth.

They may propose, remember, or explain decisions.

A decision becomes authoritative only when written into the correct repo document and approved.

### 9. Git / GitHub Audit Trail

Lives in git history, branches, commits, pull requests, issues, code reviews, CI runs, release tags, and changelogs.

Git / GitHub records what actually changed. It does not decide what the game is.

Every production implementation change must be traceable through Git / GitHub to an approved READY story.

Implementation PRs must link to:
- story ID;
- relevant GDD section;
- relevant ADR or control-manifest section;
- tests and verification evidence.

Implementation PRs must explicitly state:
- what changed;
- why it changed;
- what was intentionally not changed;
- known omissions, stubs, mocks, assumptions, and deferred work;
- verification performed.

If there are no known omissions, the PR must say `No known omissions` explicitly.

CI/test failures may not be handwaved. They must be fixed or documented as human-accepted exceptions.

Agents may not use Git history as permission to continue a pattern that conflicts with approved docs.

## Conflict Rules

Written approved docs authorize work.

Git / GitHub proves what actually happened.

If approved docs and implementation diverge, the divergence is a defect until reviewed.

If implementation conflicts with game design, technical truth, or production truth, implementation stops.

If game design conflicts with worldbuilding, the conflict must be resolved or explicitly marked as a deliberate adaptation.

If chat conflicts with written docs, written docs win.

## Implementation Authorization Gate

Production Unity code may be changed only when all authorization conditions are met:

- the relevant design behavior is covered by an approved GDD section;
- the relevant technical approach is covered by an approved ADR, architecture section, or control-manifest rule;
- the work is represented by a READY story, not only an epic or chat instruction;
- the story links to the exact GDD and technical sections it depends on;
- acceptance criteria and verification evidence are defined before implementation;
- the ambiguity check has passed;
- the work is done on a traceable branch and reviewed through Git / GitHub.

If any condition fails, implementation does not start. The correct action is to revise the story, GDD, ADR, or control manifest.

## Ambiguity Check

The ambiguity check is a required pre-implementation review that asks whether an implementer can complete the story without inventing design, architecture, content, balance, or UX decisions.

A story fails the ambiguity check if implementation would require the agent to guess any of the following:

### Design Ambiguity

- exact player-facing rule;
- formula, value, range, or tuning knob;
- state transition;
- edge-case behavior;
- win/loss, reward, cost, cooldown, limit, or failure condition;
- relationship to another system;
- whether a behavior is MVP, vertical-slice, prototype-only, or full-vision.

### Technical Ambiguity

- Unity scene, prefab, ScriptableObject, data file, service, or system ownership;
- folder/module location;
- API boundary;
- persistence/save behavior;
- event/messaging pattern;
- deterministic vs non-deterministic behavior;
- test layer required: unit, edit-mode, play-mode, integration, manual Unity check;
- whether code is prototype, production, editor-only, runtime, or test-only.

### UX / Content Ambiguity

- what the player sees;
- required feedback, tooltip, HUD state, animation, sound, or placeholder;
- naming visible to the player;
- icon/art/audio placeholder policy;
- accessibility or readability requirement.

### Scope Ambiguity

- whether the story includes adjacent behavior;
- whether stubs/mocks are allowed;
- what is intentionally out of scope;
- what omissions must be declared in the PR;
- whether existing behavior may be refactored or only extended.

### Canon / Lore Ambiguity

- whether a lore element is approved for game use;
- whether a faction, place, term, or cultural reference is safe to expose to players;
- whether game design intentionally adapts or overrides worldbuilding.

A story passes the ambiguity check only when:

- all required decisions are answered in approved docs or the story itself;
- any remaining unknowns are explicitly marked `out of scope`, `stubbed`, `mocked`, or `human-approved assumption`;
- no unresolved question would cause the agent to invent mechanics, architecture, player-facing names, canon, balance, or UX.

Required story field:

```md
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
```

If status is `FAIL`, the story is not READY.

## Story Readiness Standard

A production story is READY only when it is small enough to implement safely and specific enough that an agent cannot accidentally design the game while coding.

A READY story must include all of the following:

### Identity

- stable story ID;
- clear title;
- story type: `Logic`, `Integration`, `Visual/Feel`, `UI`, `Config/Data`, `Content`, `Tooling`, `Test`, or `Playtest`;
- owning epic;
- current status.

### Intent

The story must state the user/player/system value in plain language.

Use this form unless another form is clearer:

```md
As a [player/designer/system], I want [capability], so that [value].
```

### Source Requirements

The story must link to exact approved source sections:

- GDD path and section/rule;
- ADR, architecture section, or control-manifest rule;
- relevant UX/content/art rule, if applicable;
- relevant worldbuilding/design-bridge source, if lore-facing;
- parent epic.

A vague reference such as `see tactical combat GDD` is not enough. The story must identify the exact section or rule being implemented.

### Implementation Scope

The story must list what is in scope as concrete implementation tasks.

The story must also list what is out of scope. Adjacent behavior is out of scope unless explicitly included.

If the story permits stubs, mocks, placeholders, temporary data, or editor-only scaffolding, those must be named explicitly.

### Acceptance Criteria

Acceptance criteria must be observable and testable.

Good criteria describe externally verifiable behavior:

- given state X, when action Y occurs, result Z happens;
- invalid input A is rejected with feedback B;
- data file C produces runtime state D;
- UI element E displays value F under condition G.

Bad criteria are vague internal intentions:

- `make it feel good`;
- `support tactical combat`;
- `clean up the code`;
- `make it scalable`;
- `implement the system`.

### Verification Requirements

The story must say how DONE will be proven.

Verification may include:

- unit tests;
- Unity edit-mode tests;
- Unity play-mode tests;
- integration tests;
- data validation tests;
- manual Unity scene/prefab checks;
- screenshot or video evidence;
- performance measurement;
- playtest notes;
- CI run link.

If a test type is not applicable, the story must say `N/A` and explain why.

### Ambiguity Check

The story must include the required ambiguity-check field.

Status must be `PASS` before implementation starts.

### Branch / PR Requirements

The story must define expected Git / GitHub traceability:

- branch naming pattern;
- PR title pattern;
- required linked story ID;
- required linked source docs;
- required evidence summary;
- required omissions section.

A production story is not DONE until its PR explicitly lists known omissions, stubs, mocks, assumptions, deferred work, or `No known omissions`.

### Human Approval

A story may be drafted by an agent, but READY status requires human approval or an explicitly delegated human-approved gate.

Agents may mark a story as `NEEDS WORK` or `BLOCKED`.

Agents may not self-approve ambiguous stories as READY.

## Story DONE Standard

A story is DONE only when:

- implementation matches the approved story scope;
- acceptance criteria pass;
- required verification evidence exists;
- no unauthorized design or architecture decisions were introduced;
- omissions/stubs/mocks/deferred work are explicitly documented;
- PR/code review is complete;
- CI passes or human-approved exceptions are documented;
- any required docs were updated in the correct source-of-truth layer.

DONE means the story was implemented as authorized. It does not mean the broader epic, system, or feature is complete unless the story explicitly says so.

## Epic Standard

An epic defines a coherent capability or milestone slice, but it is not an implementation ticket.

Epics may:

- group related stories;
- describe the player/system value of a capability;
- define scope boundaries;
- identify required GDDs, ADRs, assets, and dependencies;
- track open questions and risks;
- define milestone readiness;
- sequence stories;
- summarize progress.

Epics may not:

- authorize production implementation directly;
- replace READY stories;
- hide ambiguous design decisions;
- bundle unrelated work because it is convenient;
- let agents figure out missing details;
- be marked complete unless all required child stories and evidence are complete.

Hard rule: agents and Codex may not implement an epic. They may only implement READY stories inside an epic.

## Epic Required Fields

Each epic must include:

### Epic Identity

- stable epic ID;
- clear title;
- status;
- priority tier: `MVP`, `Vertical Slice`, `Alpha`, or `Full Vision`;
- phase;
- owner;
- related systems.

### Capability Goal

A short explanation of what capability the epic creates.

Example: `Enable the player to move a Champion across a strategic region map, preview reachable sites, spend movement points, and end the turn with predictable state changes.`

### Player / Design Value

Why this epic matters to the game.

This should connect to at least one project pillar.

### Epic Source Requirements

The epic must list relevant source docs:

- GDDs;
- design bridges;
- UX specs;
- data registry docs;
- ADRs or control-manifest sections;
- worldbuilding links, if lore-facing.

An epic may depend on draft docs, but child stories cannot become READY until their exact source requirements are approved.

### Epic Scope

The epic must separate:

- `In scope`: capabilities this epic intends to deliver;
- `Out of scope`: adjacent capabilities explicitly excluded;
- `Deferred`: known future work not part of this epic.

### Child Stories

The epic must list child stories with status:

- Draft;
- NEEDS WORK;
- READY;
- IN PROGRESS;
- REVIEW;
- DONE;
- BLOCKED.

Stories should be small enough to implement independently.

### Epic Dependencies

The epic must list:

- upstream epics;
- required GDDs;
- required technical decisions;
- required data/assets;
- required tools/packages;
- blocking open questions.

### Epic Risks

The epic must identify:

- design risks;
- technical risks;
- UX/readability risks;
- scope risks;
- lore/cultural/IP risks;
- testing risks.

Each major risk should have a mitigation or owner.

### Epic Gate Status

The epic must state whether it is:

- `Draft`: rough container, not ready for story work;
- `Design Ready`: source design is clear enough to draft stories;
- `Technically Ready`: architecture/control rules exist;
- `Story Ready`: child stories can be made READY;
- `In Production`: READY stories are being implemented;
- `Complete`: all required child stories are DONE and evidence is reviewed;
- `Blocked`: cannot proceed until named blockers are resolved.

## Epic Readiness Gate

An epic may enter production only when:

- capability goal is clear;
- relevant GDD sections exist;
- relevant technical decisions exist or are explicitly N/A;
- scope and out-of-scope are explicit;
- child stories are identified;
- dependencies are known;
- major risks are documented;
- at least one child story can pass the Story Readiness Standard.

If no child story can become READY, the epic is not production-ready.

## Epic DONE Standard

An epic is DONE only when:

- all required child stories are DONE;
- required verification evidence exists;
- unresolved omissions are documented;
- docs have been updated in the correct source-of-truth layer;
- playtest/QA evidence exists if required;
- no open blocker remains hidden;
- human review accepts the epic as complete.

DONE for an epic means the intended capability slice is complete. It does not mean the full system is complete unless the epic explicitly covers the full system.

## Epic Anti-Patterns

Invalid epic behavior:

- `Build tactical combat.`
- `Implement strategic map.`
- `Make UI good.`
- `Add factions.`
- `Set up Unity.`
- `Codex should figure out architecture.`
- `Do whatever is needed for MVP.`

Valid epic framing:

- `Strategic Map MVP: Champion movement, site preview, and end-turn state.`
- `Tactical Combat MVP: two-faction skirmish with movement, attack, defeat, and battle result.`
- `Intel Resource MVP: earn typed Intel from sites and spend it on approved asset upgrades.`
- `Unity Foundation: project layout, test framework, data-loading skeleton, and CI smoke check.`

## Control Manifest Standard

The control manifest is the mandatory implementation rulebook for Codex and all coding agents.

It lives at `docs/architecture/control-manifest.md`.

The manifest is not a GDD, ADR, story, or test plan. It constrains how implementation happens.

Core rule: Codex is an implementer, not a designer or architect.

The control manifest must define:

1. Implementation Authority
   - agents implement only READY stories;
   - agents may not implement from chat, worldbuilding, epics, drafts, or assumptions;
   - agents may not invent design, architecture, UX, balance, names, canon, assets, or content.

2. Source Reading Order
   - READY story;
   - linked GDD sections;
   - linked ADR / architecture sections;
   - control manifest;
   - linked UX / art / content docs;
   - linked worldbuilding or design-bridge docs, if lore-facing;
   - relevant existing code and tests.

3. Unity Project Rules
   - Unity version;
   - render pipeline;
   - target platform;
   - project and folder layout;
   - assembly definitions;
   - scene and prefab ownership;
   - ScriptableObject and data policy;
   - input system;
   - save/load boundary;
   - package policy;
   - prototype vs production-code policy.

4. Architecture Boundaries
   - approved architecture patterns only;
   - no new global state, event buses, service locators, DI containers, serialization systems, save systems, asset-loading patterns, or module boundaries without approval;
   - no unrelated refactors hidden inside feature stories;
   - no duplicate parallel systems.

5. Data and Tuning
   - no hardcoded tunable gameplay values unless explicitly approved;
   - approved registries/config/data assets own entities, stats, formulas, costs, rewards, and tuning knobs;
   - temporary data must be marked placeholder and listed in PR omissions.

6. Testing and Verification
   - every implementation story needs evidence;
   - logic stories require automated tests unless explicitly N/A;
   - data/config stories require validation tests or scripts;
   - Unity scene, prefab, and UI stories require manual Unity verification evidence;
   - visual/feel stories require screenshot, video, or defined review protocol.

7. Scope Control
   - no adjacent mechanics because they seem useful;
   - no full-vision features promoted into MVP without gate approval;
   - no public names, lore terms, faction framing, cultural references, or player-facing text changes unless the story explicitly allows them.

8. Documentation Rules
   - behavior changes require correct doc updates or an explicit reason no update is needed;
   - stubs, mocks, placeholders, assumptions, deferred work, known omissions, and human-approved exceptions must be documented.

9. Git / GitHub Rules
   - story-scoped branches;
   - story-scoped commits;
   - PRs link story ID, GDD section, ADR/control rule, and evidence;
   - PRs include omissions or explicitly state `No known omissions`;
   - no direct push to main for production work.

10. Stop Conditions
   - story is not READY;
   - work is an epic, not a story;
   - ambiguity check is FAIL;
   - linked docs are missing or conflicting;
   - gameplay behavior or Unity architecture is ambiguous;
   - implementation would require inventing design or architecture;
   - required tests or verification cannot be performed;
   - unrelated Git changes, legal/IP/cultural risk, or asset-provenance risk appears.

Control Manifest DONE standard:

- rules are short and operational;
- agents can follow them without interpretation;
- stop conditions are explicit;
- Unity unknowns are marked as blockers or placeholders;
- every production story can reference the manifest;
- the manifest supports, but does not replace, GDDs, ADRs, stories, and tests.

## Phases

1. Concept
   - Define fantasy, audience, pillars, loops, MVP, vertical slice, risks.
   - Output: `design/gdd/game-concept.md`, `design/gdd/game-pillars.md`.
   - Gate: Concept -> Systems Design.

2. Systems Design
   - Map explicit and implicit systems.
   - Sort by dependency layer and priority tier.
   - Write implementation-grade system GDDs.
   - Gate: Systems Design -> Technical Setup.

3. Technical Setup
   - Pin Unity version and architecture rules.
   - Maintain `docs/architecture/unity-technical-scheme.md` as the Unity boundary document.
   - Write ADRs, control manifest, test strategy.
   - Gate: Technical Setup -> Pre-Production.

4. Pre-Production
   - Build throwaway prototypes and vertical-slice candidates.
   - Create epics/stories only after GDDs and architecture are usable.
   - Run playtests.
   - Gate: Pre-Production -> Production.

5. Production
   - Implement READY stories in sprints.
   - Require traceability and verification evidence.
   - Gate: Production -> Polish.

6. Polish
   - Balance, UX, accessibility, performance, onboarding, content audit.
   - Gate: Polish -> Release.

7. Release
   - Release checklist, patch/rollback plan, known issues, launch material.

## Review intensity

Default: Lean.
Use Full for:
- game concept approval;
- systems index approval;
- MVP GDD approval;
- pre-production readiness;
- production readiness;
- release readiness.

## Handoff rule

No implementation work unless the relevant story is READY and references approved GDDs/ADRs/control rules.
