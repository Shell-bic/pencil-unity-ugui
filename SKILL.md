---
name: pencil-unity-ugui
description: Systematic UI-to-engineering conversion: infer UI system structure first, then convert it into Unity engineering form.
metadata:
  short-description: Systematic UI-to-engineering conversion for Unity uGUI based on reasoning-first methodology.
---

# Pencil Unity uGUI

> [!CAUTION]
> **CRITICAL MISSIONS (核心使命与限制):**
> 1. **该 skill 不是把设计稿直接翻译成 screen/page。它要求 agent 先推导 UI 系统结构，再决定采用何种 Unity 工程组织形式！**
> 2. **禁止跳过全局结构分析直接进入 hierarchy / asset / anchor。** 
> 3. **If structure is not explicitly inferred, the agent must NOT proceed to hierarchy planning or asset placement.**
> 4. **禁止默认把界面当成 page-routing 或 shell-screen 系统。**
> 5. **禁止在未推导前套用 Screen_* / UIRouter / UIScreenController 模板。**

This is a `design-translation` and `system-reasoning` skill, not a generic uGUI authoring skill.
If the user only wants to hand-build `Canvas/Button/Text/Image` without a Pencil angle, prefer general Unity UI skills instead.

## Non-goals
Treat these as exclusions unless requested:
- Do not use for `UI Toolkit`, `UXML`, `USS`, or `UIDocument`
- Do not describe `RectTransform` as if it were browser `Flexbox`
- Do not apply a fixed-screen exhibition shell to responsive app layouts
- Do not claim pixel-perfect parity without screenshot-based verification

## Tool split
Use `Pencil MCP` for reading, inspecting, finding repetition, and classifying elements.
Use `Unity Skills` for creating structures, anchors, layout groups, and hooking up behavior based on the reasoning output.

## Workflow Pipeline (Reasoning First)

1. **Global System Analysis**: Scan the whole document. Confirm the fundamental architecture. Do not assume page-routing.
2. **Engineering Architecture Planning**: Decide whether to use pages / panels / overlays / flow / mixed structure.
3. **Reusable Component & Interaction Extraction**: Identify logical boundaries. Do not directly reuse visual elements before confirming interaction roles.
4. **Layout / Asset Placement Planning**: Decide anchors, simple vs sliced assets, and hierarchy grouping.
5. **Implementation**: Only after all reasoning is confirmed.

## Stage Locks (阶段锁)
- 未完成 Global Structure Inference → 不得进入 hierarchy 或 asset placement
- 未完成 Region Role Map → 不得决定 controller ownership
- 未完成 Interaction Model Inference → 不得决定 route / state / overlay 方案

## Failure Conditions (失败条件)
Any of the following makes the output **invalid** and requires a redo:
- If hierarchy is created first, then structure is reverse-engineered to justify it
- If `Screen_*` / `UIRouter` / `UIScreenController` naming appears without a proven routed multi-page architecture
- If visually similar elements are merged into shared components without verifying their interaction semantics are identical
- If a "shell" is assumed without evidence that multiple views demonstrably share persistent structural regions

## Files to read when needed

### Core Method
- For the end-to-end execution checklist: [references/core-method/workflow-checklist.md](references/core-method/workflow-checklist.md)
- For the required reasoning-first answer shape: [references/core-method/output-contract.md](references/core-method/output-contract.md)

### Implementation Rules
- For anchor selection and RectTransform strategy: [references/implementation-rules/anchor-rules.md](references/implementation-rules/anchor-rules.md)
- For slicing and text-vs-image decisions: [references/implementation-rules/asset-rules.md](references/implementation-rules/asset-rules.md)
- For Unity component mapping (guidelines only): [references/implementation-rules/component-rules.md](references/implementation-rules/component-rules.md)
- For structural layout conversion logic: [references/implementation-rules/layout-conversion-rules.md](references/implementation-rules/layout-conversion-rules.md)
- For prefab boundaries and controller ownership: [references/implementation-rules/prefab-binding-rules.md](references/implementation-rules/prefab-binding-rules.md)
- For naming conventions (ensure they match the inferred structure): [references/implementation-rules/naming-rules.md](references/implementation-rules/naming-rules.md)
- For content assignment and runtime binding strategy: [references/implementation-rules/data-binding-rules.md](references/implementation-rules/data-binding-rules.md)
- For visual styling elements: [references/implementation-rules/typography-visual-rules.md](references/implementation-rules/typography-visual-rules.md)
- For known bad patterns and false equivalences: [references/implementation-rules/anti-patterns.md](references/implementation-rules/anti-patterns.md)

### Templates & Examples
- Use `assets/engineering-plan-template.md` as the primary structural planner.
- Use `assets/routing-structure-template.yaml` ONLY if a true routed system was inferred.
- Review `examples/` for exhibition-specific shell patterns and trigger calibrations.

If code or Unity mutation is requested, do not stop at explanation. Produce the hierarchy, scripts, or editor actions that are actually needed based on your structural reasoning.
