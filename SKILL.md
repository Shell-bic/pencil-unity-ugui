---
name: pencil-unity-ugui
description: Systematic UI-to-engineering conversion using Pencil MCP. Translates designs into Unity uGUI architectures based on rigorous structural reasoning first, rather than applying default templates.
metadata:
  short-description: Systematic UI-to-engineering conversion for Unity uGUI based on reasoning-first methodology.
---

# Pencil Unity uGUI

> [!CAUTION]
> **CRITICAL RESTRICTIONS (核心限制):**
> 1. **禁止跳过全局结构分析直接进入 hierarchy / asset / anchor。** (Do not skip global structural analysis to jump straight into hierarchy, assets, or anchors.)
> 2. **禁止默认把界面当成 page-routing 或 shell-screen 系统。** (Do not default to assuming the interface is a page-routing or shell-screen system.)
> 3. **禁止因为已有模板存在，就在未推导结构前直接套 Screen_* / UIRouter / UIScreenController。** (Do not blindly apply pre-existing screen or router templates before deducing the actual required structure.)

This is a `design-translation` and `system-reasoning` skill, not a generic uGUI authoring skill.

If the user only wants to hand-build `Canvas/Button/Text/Image` without a Pencil angle, prefer general Unity UI skills instead.

Use this skill when the target output is `Unity uGUI`, and the source of truth is:
- a `Pencil MCP` design
- a screenshot/layout spec that requires structural reasoning

This skill exists to keep later agents from mixing `uGUI`, `UI Toolkit`, browser layout mental models, and generic scene building.

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

1. **Target Confirmation**: Verify the target is uGUI and the goal (planning vs execution).
2. **Global Document Scanning**: Use Pencil to scan the whole file. Identify all artboards/frames.
3. **Global Semantic Analysis & Structural Reasoning**: (CRITICAL STEP)
   - What is the fundamental architecture? Is it a continuous workflow, a single-screen state machine, a HUD overlay, or actually a multi-page routed app? Do not assume page-routing.
4. **Region Role Inference**: Map the semantic roles of the regions before assigning Unity hierarchy types.
5. **Interaction Model Inference**: Determine if interactions trigger state swaps, overlays, external system events, or actual scene/page routing.
6. **Classification**: Classify nodes based on the verified structural intent.
7. **Layout & Parent Strategy**.
8. **Anchor & Asset Strategy**.
9. **Component & Prefab Bounds**.
10. **Output Planning**: Present the reasoning and plans using [references/output-contract.md](references/output-contract.md).

## Files to read when needed
- Implementation rules: `unity-skills` and `unity-ui`
- Anchor selection: [references/anchor-rules.md](references/anchor-rules.md)
- Asset slicing: [references/asset-rules.md](references/asset-rules.md)
- Component selection: [references/component-rules.md](references/component-rules.md) (Note: treat as guidelines, not forced types)
- Prefab/Script boundaries: [references/prefab-binding-rules.md](references/prefab-binding-rules.md)
- Output contract: [references/output-contract.md](references/output-contract.md)
- Workflow checklist: [references/workflow-checklist.md](references/workflow-checklist.md)
- Anti-patterns: [references/anti-patterns.md](references/anti-patterns.md)

If code or Unity mutation is requested, do not stop at explanation. Produce the hierarchy, scripts, or editor actions that are actually needed based on your structural reasoning.
