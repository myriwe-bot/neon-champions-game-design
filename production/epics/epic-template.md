---
title: Epic Template
type: epic
status: draft
phase: pre-production
owner: shared
created: 2026-05-22
updated: 2026-05-25
source_lore: []
related: [design/workflow, docs/architecture/testing-strategy, docs/architecture/ci-build-automation, production/stories/story-template]
approval: pending
---

# Epic: [EPIC-ID] [Name]

## Status

Draft | Design Ready | Technically Ready | Story Ready | In Production | Complete | Blocked

## Priority tier

MVP | Vertical Slice | Alpha | Full Vision

## Phase

Concept | Systems Design | Technical Setup | Pre-Production | Production | Polish | Release

## Owner

Human | Agent-assisted | Shared

## Related systems

- ...

## Capability goal

What coherent capability or milestone slice this epic creates.

Example:
`Enable the player to move a Champion across a strategic region map, preview reachable sites, spend movement points, and end the turn with predictable state changes.`

## Player / design value

Why this epic matters to the game.

Relevant pillars:
- [ ] Cyberpunk strategy/RPG
- [ ] Infrastructure-first conflict
- [ ] Champions as legitimacy and force projection
- [ ] Intel as secrets turned into power
- [ ] Dirty information
- [ ] HoMM-like exploration, capture, and tactical escalation
- [ ] Other:

## Source requirements

An epic may depend on draft docs, but child stories cannot become READY until their exact source requirements are approved.

- GDDs:
- Design bridges:
- UX specs:
- Data registry docs:
- ADRs / architecture docs / control-manifest sections:
- Worldbuilding links, if lore-facing:
- Reference/legal/cultural constraints, if relevant:

## Scope

### In scope

Capabilities this epic intends to deliver:

- ...

### Out of scope

Adjacent capabilities explicitly excluded:

- ...

### Deferred

Known future work not part of this epic:

- ...

## Child stories

Agents and Codex may not implement this epic directly. They may only implement READY child stories.

| Story | Status | Type | Depends On | Evidence |
|---|---|---|---|---|
| [STORY-ID] [Name] | Draft | Logic | ... | ... |

Allowed story statuses:
- Draft
- NEEDS WORK
- READY
- IN PROGRESS
- REVIEW
- DONE
- BLOCKED

## Dependencies

- Upstream epics:
- Required GDDs:
- Required technical decisions:
- Required testing/evidence strategy:
- Required CI/build automation:
- Required agent instruction scopes / AGENTS.md updates:
- Required data/assets:
- Required tools/packages:
- Blocking open questions:

## Risks

| Risk | Type | Impact | Mitigation / Owner |
|---|---|---|---|
| ... | Design / Technical / UX / Scope / Lore-Cultural-IP / Testing | ... | ... |

## Epic readiness gate

An epic may enter production only when all items are true:

- [ ] Capability goal is clear.
- [ ] Relevant GDD sections exist.
- [ ] Relevant technical decisions exist or are explicitly N/A.
- [ ] Required test/evidence layers are known for expected child story types.
- [ ] Required CI/build checks are known for expected child story types, or explicitly N/A with reason.
- [ ] Required agent instruction scopes / AGENTS.md updates are known, or explicitly N/A with reason.
- [ ] Scope and out-of-scope are explicit.
- [ ] Child stories are identified.
- [ ] Dependencies are known.
- [ ] Major risks are documented.
- [ ] At least one child story can pass the Story Readiness Standard.

If no child story can become READY, the epic is not production-ready.

## Epic DONE gate

An epic may be marked Complete only when all items are true:

- [ ] All required child stories are DONE.
- [ ] Required verification evidence exists.
- [ ] Required automated tests, validators, PlayMode/smoke evidence, and manual evidence are complete or accepted as documented exceptions.
- [ ] Unresolved omissions are documented.
- [ ] Docs have been updated in the correct source-of-truth layer.
- [ ] Playtest/QA evidence exists if required.
- [ ] No open blocker remains hidden.
- [ ] Human review accepts the epic as complete.

## Anti-pattern check

Invalid epic behavior:
- [ ] This epic authorizes production implementation directly.
- [ ] This epic replaces READY stories.
- [ ] This epic hides ambiguous design decisions.
- [ ] This epic bundles unrelated work for convenience.
- [ ] This epic asks agents to figure out missing details.

If any box above is checked, the epic needs revision.

## Verdict

Draft | Design Ready | Technically Ready | Story Ready | In Production | Complete | Blocked
