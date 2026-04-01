# Workflow Checklist

Use this file to guide the systematic UI-to-engineering conversion from Pencil design to Unity uGUI.
**CRITICAL**: Do not skip the Global Structural Reasoning stage.

## Contents
- Stage 1: Confirm target
- Stage 2: Read the design
- Stage 3: Global Semantic Analysis & Structural Reasoning (CRITICAL)
- Stage 4: Region Role Map Inference
- Stage 5: Interaction Model Inference
- Stage 6: Classify Nodes
- Stage 7: Layout and Anchor Strategy
- Stage 8: Asset & Typography Strategy
- Stage 9: Component & Binding Boundaries
- Stage 10: Hierarchy & Implementation

## Stage 1: Confirm target
Confirm the technology is `uGUI`. Confirm if the user wants purely architectural planning, or editor implementation.

## Stage 2: Read the design
Inspect top-level frames, bounds, and repeated structures using Pencil MCP. Do not immediately assume multiple frames equals multiple screens. They could be state panels, overlays, or reference boards.

## Stage 3: Global Semantic Analysis & Structural Reasoning (CRITICAL)
Before deciding on any hierarchy or code structure, you MUST deduce the systemic nature of the design.
Questions to ask:
- Is this a single-view state machine?
- Is this a multi-step continuous workflow wizard?
- Is this a HUD overlay over 3D content?
- Is this a true routed multi-page application?
Do NOT default to "shell-screen" or "page-routing" architecture unless the design explicitly justifies it.

## Stage 4: Region Role Map Inference
Map the structural regions not by their Unity component types, but by their semantic roles.
Examples: "Global Status Indicator", "Contextual Action Bar", "Data Visualization Area".
Do NOT prematurely name them `Shell_LeftNav` or `Shell_Header` unless the system reasoning warrants a shell pattern.

## Stage 5: Interaction Model Inference
Based on the visual clues, what do the interactions drive?
- Simple local UI state toggles (e.g., expanding a list)?
- Global application context switches?
- External hardware/system commands?
Determine the level of the controller needed (e.g., StateGroupController, FlowDirector) instead of defaulting to `UIScreenController`.

## Stage 6: Classify Nodes
Now classify the nodes structurally based on the reasoning from Stages 3-5.
- Backgrounds, Containers, Decorators, Interactive Hotspots, Live Data text.

## Stage 7: Layout and Anchor Strategy
Choose `fixed-placement` vs `layout-group`.
Use anchor-rules to place elements structurally before tuning raw coordinates.

## Stage 8: Asset & Typography Strategy
Determine Simple vs Sliced sprites, and text stylings.

## Stage 9: Component & Binding Boundaries
Based on the Interaction Model (Stage 5), decide where prefabs and controllers should live. Do not map everything to a central router if the system is locally state-driven.

## Stage 10: Hierarchy & Implementation
Finally, create or describe the hierarchy. Only use `Screen_`, `Region_` prefixes if they match the deduced reasoning. Avoid boilerplate forced templates.
