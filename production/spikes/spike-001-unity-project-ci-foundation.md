---
title: SPIKE-001 Unity Project + CI Foundation Spike
type: spike
status: approved
phase: technical-setup
owner: shared
created: 2026-05-27
updated: 2026-05-27
source_lore: []
related:
  [
    docs/architecture/unity-technical-scheme,
    docs/architecture/technical-decision-priorities,
    docs/architecture/ci-build-automation,
    docs/architecture/testing-strategy,
    docs/architecture/control-manifest,
    docs/architecture/codex-agent-instructions,
    docs/architecture/unity-repo-agents-template,
  ]
approval: approved
---

# SPIKE-001 Unity Project + CI Foundation Spike

## Decision

Run the first Unity spike as a technical foundation spike, not a gameplay prototype.

## Core Question

Can we create the Neon Champions Unity 6.4 project with the approved technical defaults, verify it through CI, and establish the minimum folder/test/automation scaffold without making production gameplay decisions?

## Primary Goals

1. Confirm Unity version availability:
   - preferred: `6000.4.8f1`;
   - if unavailable: stop and request approval for replacement.

2. Create Unity project with approved defaults:
   - Unity 6.4;
   - URP;
   - desktop/PC target first;
   - Unity Input System;
   - 2.5D-compatible setup, but no final camera/grid decision.

3. Establish folder scaffold:
   - `Assets/NeonChampions/Runtime/Domain`;
   - `Assets/NeonChampions/Runtime/Application`;
   - `Assets/NeonChampions/Runtime/Presentation`;
   - `Assets/NeonChampions/Runtime/Infrastructure`;
   - `Assets/NeonChampions/Runtime/Data`;
   - `Assets/NeonChampions/Editor`;
   - `Assets/NeonChampions/Tests/EditMode`;
   - `Assets/NeonChampions/Tests/PlayMode`;
   - `Assets/NeonChampions/Scenes`.

4. Establish assembly scaffold:
   - `NeonChampions.Domain`;
   - `NeonChampions.Application`;
   - `NeonChampions.Infrastructure`;
   - `NeonChampions.Presentation`;
   - `NeonChampions.Tests.EditMode`;
   - `NeonChampions.Tests.PlayMode`.

5. Add minimal tests:
   - one EditMode smoke test proving the test runner works;
   - one PlayMode smoke test if feasible;
   - one placeholder validator command/test proving the validation path exists.

6. Add CI:
   - GitHub Actions workflow;
   - Unity compile/check;
   - EditMode test run;
   - validator run;
   - PlayMode smoke if feasible;
   - CI evidence linked in PR/spike notes.

7. Add agent instruction scaffold:
   - root Unity repo `AGENTS.md` based on `docs/architecture/unity-repo-agents-template.md`;
   - initial scoped `AGENTS.md` files where practical for Domain, Application, Presentation, Infrastructure, Data, Tests, Editor, and evidence;
   - document any template deviations caused by actual Unity project layout.

## In Scope

- Unity project creation.
- URP project setup.
- Folder and assembly scaffold.
- Test runner scaffold.
- CI workflow scaffold.
- Root/scoped AGENTS.md scaffold for the future Unity repo.
- Minimal "does this run?" tests.
- Documentation of exact Unity version/tooling discovered.

## Out of Scope

- Tactical combat implementation.
- Strategic map implementation.
- Champion mechanics.
- Faction/unit stats.
- Save/load implementation.
- Localization package decision unless Unity requires a harmless placeholder.
- Final data schema.
- Final map/scenario structure.
- Real art pipeline.
- Production gameplay code.

## Allowed Placeholder Code

- Trivial smoke classes/tests only.
- Example validator stub only.
- Empty/placeholder scene only if needed for PlayMode/CI.

## Not Allowed

- Implementing real mechanics "just to test".
- Hardcoding game rules.
- Creating production ScriptableObject schemas.
- Choosing save/load format.
- Choosing localization package.
- Deciding final grid/camera/tile structure.
- Treating prototype folders/scenes as production-approved gameplay structure beyond the approved scaffold.

## Success Criteria

- Unity version is confirmed or blocked with clear reason.
- Project opens/compiles.
- Approved folder scaffold exists.
- Assembly definitions exist and enforce intended dependency direction at least minimally.
- EditMode smoke test passes locally and/or in CI.
- CI workflow exists and runs.
- CI result is linked as evidence.
- Spike report states what is reusable vs throwaway.
- No unauthorized gameplay/design decisions were introduced.

## Failure Criteria

- Approved Unity version unavailable and no replacement approved.
- CI cannot be configured without unresolved license/runner issue.
- Test runner cannot be made to run.
- Folder/assembly structure causes Unity problems requiring architecture revision.
- Spike requires unapproved data/save/localization/input decisions.

## Reusable Outputs

Candidate production foundation if reviewed and accepted:

- Unity project scaffold.
- Folder/assembly layout.
- CI workflow.
- AGENTS.md instruction scaffold.
- Smoke tests.

## Throwaway Outputs

- Placeholder scenes.
- Placeholder validator content.
- Temporary sample objects.
- Example MonoBehaviours used only to prove PlayMode wiring.

## Agent Stop Conditions

Codex/agent must stop and report if:

- Unity `6000.4.8f1` is unavailable;
- CI requires credentials/license decisions not already available;
- AGENTS.md scaffold conflicts with approved architecture/control rules;
- package choices beyond approved defaults are needed;
- test scaffolding requires changing architecture rules;
- any gameplay decision seems necessary.

## Evidence Requirements

The spike completion report must include:

- Unity version found/used;
- project creation command or method;
- CI run link or exact blocker;
- AGENTS.md files created and any deviations from template;
- tests/checks run;
- pass/fail summary;
- reusable outputs;
- throwaway outputs;
- omissions/stubs/placeholders;
- explicit statement that no production gameplay was implemented.

## Verdict

APPROVED.
