---
title: Codex PR Review Checklist
type: checklist
status: approved
phase: production
owner: shared
created: 2026-05-27
updated: 2026-05-27
source_lore: []
related:
  [
    docs/architecture/control-manifest,
    docs/architecture/codex-agent-instructions,
    docs/architecture/multi-agent-operating-model,
    docs/architecture/testing-strategy,
    docs/architecture/ci-build-automation,
    production/stories/story-template,
  ]
approval: approved
---

# Codex PR Review Checklist

Use this checklist for future Codex/agent implementation PRs in the Unity repo.

## 1. Authority Check

- [ ] PR links an approved spike or READY story.
- [ ] PR does not implement an epic directly.
- [ ] PR links exact GDD sections or states N/A with reason.
- [ ] PR links exact ADR/control-manifest sections.
- [ ] Relevant root/scoped `AGENTS.md` files were followed.
- [ ] Human-approved exceptions are explicitly listed.

Reject if implementation is based only on chat, memory, an epic, draft docs, or worldbuilding.

## 2. Scope Check

- [ ] Changes match approved in-scope items.
- [ ] Out-of-scope items were not implemented.
- [ ] No adjacent mechanics were added for convenience.
- [ ] No unapproved balance, UX, lore, content, names, assets, package choices, data schemas, localization, save/load, or architecture decisions were introduced.
- [ ] Unrelated cleanup is not bundled.

## 3. Unity Asset Check

- [ ] Changed `.unity`, `.prefab`, `.asset`, `.controller`, `.meta`, package, and ProjectSettings files are listed.
- [ ] Scene/prefab changes are authorized by the story/spike.
- [ ] No `.meta` files were deleted accidentally.
- [ ] No missing script references were introduced, where checkable.
- [ ] Prefab/scene fields do not define unapproved gameplay rules.
- [ ] Generated/tool-created changes are disclosed.

## 4. Architecture Check

- [ ] Domain code remains testable without scenes/prefabs/MonoBehaviours/ScriptableObjects.
- [ ] `Domain` does not depend on `UnityEngine` unless explicitly approved.
- [ ] Dependency direction follows approved assembly boundaries.
- [ ] No new global state, event bus, service locator, DI container, save/load system, serialization system, asset-loading pattern, or data pipeline was introduced without approval.
- [ ] Runtime state remains serializable where relevant.

## 5. Data / Localization Check

- [ ] Static definitions, scenario data, runtime state, and save data remain separate.
- [ ] Stable IDs are used where definitions exist.
- [ ] Player-facing strings use localization keys unless explicitly prototype-only.
- [ ] Validators cover touched data/content/localization.
- [ ] No hardcoded production tunable gameplay values were added unless explicitly approved.

## 6. Testing / CI Check

- [ ] Required EditMode/domain tests exist and pass.
- [ ] Required data/content/localization validators exist and pass.
- [ ] Required PlayMode/smoke tests exist and pass, or approved temporary exception is documented.
- [ ] Visual/UX/feel evidence exists where required.
- [ ] CI link is provided once CI exists.
- [ ] CI failures are fixed or human-approved exceptions are documented.
- [ ] Production logic/bug fixes followed TDD, or exception is documented.

## 7. Evidence / Omissions Check

- [ ] PR includes exact tests/checks run.
- [ ] PR includes pass/fail summary.
- [ ] PR links manual evidence paths where applicable.
- [ ] PR includes omissions/stubs/mocks/assumptions/deferred work, or says `No known omissions`.
- [ ] PR states docs updated or explains why no docs update was needed.
- [ ] Stop-condition risks are listed, or PR says `No known stop-condition risks`.

## 8. Review Verdict

Use one verdict:

- `APPROVE`: no blocking issues.
- `REQUEST CHANGES`: fix required before merge.
- `BLOCK`: missing authority, source conflict, unsafe architecture/design change, or required evidence absent.

## Required Review Output Format

```text
Verdict: APPROVE / REQUEST CHANGES / BLOCK

Blocking issues:
- ...

Important issues:
- ...

Minor notes:
- ...

Evidence reviewed:
- ...

Scope/authority conclusion:
- ...
```
