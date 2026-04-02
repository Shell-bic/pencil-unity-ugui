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

**Minimum Verifiable Output (all required):**
1. The inferred system type (one of: single-view state machine / multi-step flow / overlay HUD / routed multi-page / mixed — with sub-type if mixed)
2. At least **one alternative type explicitly rejected** with a reason referencing visual evidence (e.g., "Not a routed system because Frame_A and Frame_B coexist on the same artboard without mutually exclusive switching")
3. A list of **visual evidence** (node names, layout patterns, or screenshot observations) supporting the inference

**Next Stage Gate:** An output missing any of the 3 items above is incomplete. Do not proceed.

---

## Stage 2: Engineering Architecture Planning
**Input:** The `GlobalStructureSummary` from Stage 1.
**Questions to Answer:**
- Based on the system type, what is the macro-level Unity format? (e.g., Persistent Shell + Swapping Panels, or 3D World Canvas HUD).
**Forbidden Actions:**
- Do NOT decide on Anchors or layout groups.
- Do NOT name components `Screen_` unless a routed multi-page architecture was explicitly proven in Stage 1.
**Output:** A `RegionRoleMap` mapping visual areas to semantic roles (e.g., "Persistent Status Bar", "Contextual Action Flyout").

**Minimum Verifiable Output (all required):**
1. A table or list mapping **every major visual area** to a semantic role
2. The macro-level Unity format chosen, with explicit link back to Stage 1 system type
3. If `Shell_*` or `Screen_*` prefixes are proposed, the Stage 1 evidence that justifies them

**Next Stage Gate:** All major visual areas must have an assigned semantic role. Unassigned areas block progress.

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

**Minimum Verifiable Output (all required):**
1. The inferred controller type(s) with justification linked to interaction patterns (not defaults)
2. A prefab boundary list: which clusters warrant extraction and why
3. For each visually similar group: confirmation that interaction semantics were verified (not assumed identical)

**Next Stage Gate:** Prefab boundaries and inferred controller roles are explicitly defined. Generic controller names without justification block progress.

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

**Minimum Verifiable Output (all required):**
1. For each major node/group: the designated parent owner
2. Anchor intent for each major region (preset name + stretch/fixed reasoning)
3. Asset decision per visual node: simple-sprite / sliced-sprite / live text / decorative-only
4. At least one layout risk or uncertainty explicitly called out

**Next Stage Gate:** Every important node has a Parent, an Anchor, and a Sprite mapping intent. Nodes without all three block progress.

---

## Stage 5: Implementation & Refinement
**Input:** The fully finalized plans from Stages 1-4.
**Questions to Answer:**
- Which steps should be executed via Unity Skills automation vs left for manual tuning?
**Forbidden Actions:**
- Do NOT execute automated hierarchy creation if any uncertainties remain in Stage 1-4.
**Output:** Automated Unity Editor actions (if requested) and a `NeedsManualConfirmation` list.

**Minimum Verifiable Output (all required):**
1. Which parts are safe for automation (and will be executed)
2. Which parts require manual confirmation (the `NeedsManualConfirmation` list)
3. Confirmation that implementation matches Stage 1–3 inferred structure (not a post-hoc justification)
4. Explicit note of any inferred-but-unverified assumptions that remain

**Next Stage Gate:** Implementation accurately reflects the structurally reasoned architecture. Any mismatch between implementation and Stage 1–3 reasoning is a failure.
