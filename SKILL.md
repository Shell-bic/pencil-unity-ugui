---
name: pencil-unity-ugui
description: Systematic Pencil-to-Unity uGUI design translation and engineering planning. Use when the task involves Pencil MCP or design-driven UI conversion for Unity uGUI, including screen structure inference, page vs panel architecture, Canvas and RectTransform hierarchy planning, anchor strategy, asset slicing, prefab boundaries, interaction mapping, or turning a .pen-style design into an implementation plan or Unity uGUI structure. Do not use for UI Toolkit unless the user explicitly asks for comparison or migration.
metadata:
  short-description: Systematic UI-to-engineering conversion for Unity uGUI based on reasoning-first methodology.
---

# Pencil Unity uGUI

> [!CAUTION]
> **CRITICAL MISSIONS (Core Mission And Limits):**
> 1. **Do not translate the design into a Unity screen or page first. Infer the UI system structure first, then decide the Unity engineering shape.**
> 2. **Do not skip global structure analysis and jump straight into hierarchy, asset, or anchor work.**
> 3. **If structure is not explicitly inferred, do not proceed to hierarchy planning or asset placement.**
> 4. **Do not default to treating the UI as a page-routing or shell-screen system.**
> 5. **Do not apply `Screen_*`, `UIRouter`, or `UIScreenController` patterns before they are earned by reasoning.**

This is a `design-translation` and `system-reasoning` skill, not a generic uGUI authoring skill.
If the user only wants to hand-build `Canvas`, `Button`, `Text`, or `Image` without a Pencil angle, prefer general Unity UI skills instead.

## Non-goals
Treat these as exclusions unless requested:
- Do not use for `UI Toolkit`, `UXML`, `USS`, or `UIDocument`
- Do not describe `RectTransform` as if it were browser `Flexbox`
- Do not apply a fixed-screen exhibition shell to responsive app layouts
- Do not claim pixel-perfect parity without screenshot-based verification

## Tool Split
Use `Pencil MCP` for reading, inspecting, finding repetition, and classifying elements.
Use `Unity Skills` for creating structures, anchors, layout groups, and hooking up behavior based on the reasoning output.

## Workflow Pipeline (Reasoning First)

1. **Global System Analysis**: Scan the whole document. Confirm the fundamental architecture. Do not assume page-routing.
2. **Engineering Architecture Planning**: Decide whether to use pages, panels, overlays, flow, or a mixed structure.
3. **Reusable Component & Interaction Extraction**: Identify logical boundaries. Do not directly reuse visual elements before confirming interaction roles.
4. **Page Truth & Shared Component Fact Lock**: Before any mutation touching shared shell regions or page-state mapping, read the current `.pen` and build a `PageTruthMap` plus a `SharedComponentFactTable`.
5. **Layout / Asset Placement Planning**: Decide anchors, simple vs sliced assets, and hierarchy grouping.
6. **Implementation**: Only after all reasoning is confirmed.

## Fact Lock Rule (Mandatory)

When the task involves any of the following, the agent must lock facts from the current Pencil source before implementation:
- A shared shell region that appears across pages, such as left navigation, top command buttons, language toggles, playback bars, or persistent side rails
- Any question of whether a given page is a landing page, a child page, an expanded navigation state, or a local content switch
- Any proportion dispute where previous Unity output or screenshots conflict with what the `.pen` currently shows

The fact lock must produce two explicit artifacts in the reasoning:
- `PageTruthMap`: For each referenced page, record the active primary item, whether secondary navigation is shown, which secondary item is selected, and which shell regions are visible or hidden
- `SharedComponentFactTable`: For each shared component family, record exact geometry and notable structural facts from the current `.pen`

If the current `.pen` is available, historical Unity screenshots or previous implementation output may be used only as comparison evidence. They must never replace the current Pencil facts as the source of truth.

## Stage Locks
- If Global Structure Inference is incomplete, do not proceed to hierarchy or asset placement
- If RegionRoleMap is incomplete, do not decide controller ownership
- If InteractionModelInference is incomplete, do not decide route, state, or overlay strategy
- If `PageTruthMap` is required but missing, do not proceed to page mapping, navigation logic, or visibility rules
- If `SharedComponentFactTable` is required but missing, do not proceed to shared shell sizing, spacing, or animation tuning

## Failure Conditions
Any of the following makes the output invalid and requires a redo:
- If hierarchy is created first, then structure is reverse-engineered to justify it
- If `Screen_*`, `UIRouter`, or `UIScreenController` naming appears without a proven routed multi-page architecture
- If visually similar elements are merged into shared components without verifying their interaction semantics are identical
- If a shell is assumed without evidence that multiple views demonstrably share persistent structural regions
- If a shared shell component such as navigation or playback is sized from historical screenshots instead of the current `.pen`
- If right-side content chips or local action buttons are inferred to be left-side navigation children without direct page evidence
- If a page is implemented with secondary navigation expanded even though the referenced Pencil page shows a landing state with no secondary menu

## Files To Read When Needed

### Core Method
- For the end-to-end execution checklist: [references/core-method/workflow-checklist.md](references/core-method/workflow-checklist.md)
- For the required reasoning-first answer shape: [references/core-method/output-contract.md](references/core-method/output-contract.md)
- For mandatory page/state and shared-shell fact locking: [references/core-method/fact-lock.md](references/core-method/fact-lock.md)

### Implementation Rules
- For anchor selection and RectTransform strategy: [references/implementation-rules/anchor-rules.md](references/implementation-rules/anchor-rules.md)
- For slicing and text-vs-image decisions: [references/implementation-rules/asset-rules.md](references/implementation-rules/asset-rules.md)
- For Unity component mapping guidelines: [references/implementation-rules/component-rules.md](references/implementation-rules/component-rules.md)
- For structural layout conversion logic: [references/implementation-rules/layout-conversion-rules.md](references/implementation-rules/layout-conversion-rules.md)
- For prefab boundaries and controller ownership: [references/implementation-rules/prefab-binding-rules.md](references/implementation-rules/prefab-binding-rules.md)
- For naming conventions: [references/implementation-rules/naming-rules.md](references/implementation-rules/naming-rules.md)
- For content assignment and runtime binding strategy: [references/implementation-rules/data-binding-rules.md](references/implementation-rules/data-binding-rules.md)
- For visual styling elements: [references/implementation-rules/typography-visual-rules.md](references/implementation-rules/typography-visual-rules.md)
- For known bad patterns and false equivalences: [references/implementation-rules/anti-patterns.md](references/implementation-rules/anti-patterns.md)

### Templates & Examples
- Use `assets/engineering-plan-template.md` as the primary structural planner
- Use `assets/routing-structure-template.yaml` only if a true routed system was inferred
- Review `examples/` for exhibition-specific shell patterns and trigger calibrations

## Pre-Implementation Validator

> [!CAUTION]
> **Before any implementation (hierarchy creation, script naming, asset placement), the agent must pass all of the following checks. If any check fails, the output is invalid and must be redone.**

### Check 1: Structure-Hierarchy Alignment
- Does every hierarchy prefix (`Screen_*`, `Shell_*`, `State_*`, `Flow_*`, `Group_*`) match the system type inferred in Stage 1?
- If `Screen_*` or `Shell_*` appears, was a routed multi-page or persistent-shell architecture explicitly proven?
- Fail condition: Any prefix that was not earned by structural reasoning

### Check 2: No Unearned Defaults
- Are `UIScreenController`, `UIRouter`, or `PageController` used anywhere?
- If yes, was a routed multi-page architecture confirmed in Stage 1?
- Fail condition: Any router or screen-controller naming without Stage 1 proof

### Check 3: Reasoning Substance
- Does the `GlobalStructureSummary` contain the inferred system type with visual evidence?
- Does it reject at least one alternative structure with reasoning?
- Does the `RegionRoleMap` assign semantic roles to all major visual areas?
- Fail condition: Single-sentence or evidence-free structural claims

### Check 4: Fact Lock Integrity
- If the task touches shared shell regions or page-state mapping, were `PageTruthMap` and `SharedComponentFactTable` produced?
- Are shared shell sizes and visibility rules derived from the current `.pen` rather than historical screenshots?
- Fail condition: Any shared shell tuning done without current Pencil facts

### Check 5: No Reverse Engineering
- Was the hierarchy designed to match the structural reasoning from the top down?
- Or was the hierarchy created first and then the reasoning written to justify it?
- Fail condition: Any sign that structure was reverse-engineered from a pre-decided hierarchy

If code or Unity mutation is requested, do not stop at explanation. Produce the hierarchy, scripts, or editor actions that are actually needed based on your structural reasoning.
