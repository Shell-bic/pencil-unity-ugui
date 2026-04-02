# Workflow Checklist (Strict Protocol)

This document is the absolute execution protocol for translating a Pencil design into Unity uGUI. 
**Agent MUST execute these 5 stages sequentially. Skipping stages is an automatic failure.**

---

## Stage 1: Global System Analysis
**Input:** The raw Pencil `.pen` file and any provided screenshots.
**Questions to Answer:**
- Is the entire design a single-view state machine, a multi-step sequence, an overlay HUD, or a routed multi-page application?
**Forbidden Actions:**
- Do NOT create any Unity hierarchy objects.
- Do NOT classify specific nodes (e.g., "This is a button").
**Output:** A confirmed `GlobalStructureSummary` defining the systemic nature of the UI.
**Next Stage Condition:** You must be able to explicitly state why the UI is NOT a different type of system (e.g., "Not a routed system because views coexist").

---

## Stage 2: Engineering Architecture Planning
**Input:** The `GlobalStructureSummary` from Stage 1.
**Questions to Answer:**
- Based on the system type, what is the macro-level Unity format? (e.g., Persistent Shell + Swapping Panels, or 3D World Canvas HUD).
**Forbidden Actions:**
- Do NOT decide on Anchors or layout groups.
- Do NOT name components `Screen_` unless a routed multi-page architecture was explicitly proven in Stage 1.
**Output:** A `RegionRoleMap` mapping visual areas to semantic roles (e.g., "Persistent Status Bar", "Contextual Action Flyout").
**Next Stage Condition:** All major visual areas must have an assigned semantic role.

---

## Stage 3: Reusable Component & Interaction Extraction
**Input:** The `RegionRoleMap`.
**Questions to Answer:**
- How does the user interact with the system? (e.g., Toggling a filter vs navigating to a new route).
- Which clusters of UI are structurally repeated and warrant Prefabs?
**Forbidden Actions:**
- Do NOT share components between visually similar elements if their semantic interaction roles differ (e.g., a tab nav button vs a list item).
- Do NOT default the controller ownership to `UIScreenController` or `UIRouter`.
**Output:** An `InteractionModelInference` defining the runtime controllers (e.g., `StateGroupController`, `OverlayManager`).
**Next Stage Condition:** Prefab boundaries and inferred controller roles are explicitly defined.

---

## Stage 4: Layout & Asset Placement Planning
**Input:** The defined components and architecture from Stages 1-3.
**Questions to Answer:**
- What are the logical parent-child relationships?
- What is the Anchor alignment strategy to fulfill the Architecture Plan?
**Forbidden Actions:**
- Do NOT use raw Canvas coordinates before defining the structural Parent and Anchor intent.
- Do NOT use LayoutGroups unless content is dynamically reflowing or strictly repeating.
**Output:** `HierarchyPlan`, `AnchorPlan`, and `AssetPlan`.
**Next Stage Condition:** Every important node has a Parent, an Anchor, and a Sprite mapping intent.

---

## Stage 5: Implementation & Refinement
**Input:** The fully finalized plans from Stages 1-4.
**Questions to Answer:**
- Which steps should be executed via Unity Skills automation vs left for manual tuning?
**Forbidden Actions:**
- Do NOT execute automated hierarchy creation if any uncertainties remain in Stage 1-4.
**Output:** Automated Unity Editor actions (if requested) and a `NeedsManualConfirmation` list.
**Next Stage Condition:** Implementation accurately reflects the structurally reasoned architecture.
