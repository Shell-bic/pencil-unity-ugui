# Workflow Checklist

Use this file to guide the systematic UI-to-engineering conversion from Pencil design to Unity uGUI.

> **CRITICAL STAGE LOCK**: Do not proceed to hierarchy planning before:
> - Global structure is defined
> - Region roles are identified
> - Interaction model is inferred
> If hierarchy or anchors are defined before structure inference, the result is invalid.

## Contents
- Stage 1: Confirm target
- Stage 2: Read the design
- Stage 3: Global System Analysis
- Stage 4: Engineering Architecture Planning
- Stage 5: Reusable Component & Interaction Extraction
- Stage 6: Layout / Asset Placement Planning
- Stage 7: Implementation

## Stage 1: Confirm target
Confirm the technology is `uGUI`. Confirm if the user wants purely architectural planning, or editor implementation.

## Stage 2: Read the design
Inspect top-level frames, bounds, and repeated structures using Pencil MCP. 

## Stage 3: Global System Analysis
Before deciding on any hierarchy or code structure, you MUST deduce the systemic nature of the design.
Questions to ask:
- Is this a single-view state machine?
- Is this a multi-step continuous workflow wizard?
- Is this a HUD overlay over 3D content?
- Is this a true routed multi-page application?

## Stage 4: Engineering Architecture Planning
Based on the Global System Analysis, determine the structural patterns used. Do not assume "shell-screen". Exhibit why certain regions are persistent or switched.

## Stage 5: Reusable Component & Interaction Extraction
Map the structural regions not by their Unity component types, but by their semantic roles.
Identify interactive components and flow directors. 
**PROHIBITION**: In completing Component Extraction, do not directly map identical visual elements to the same runtime controllers until interaction roles are proven identical.

## Stage 6: Layout / Asset Placement Planning
Now classify the nodes structurally based on the reasoning from prior stages. Determine Anchor strategy and fixed-placement vs LayoutGroup rules.

## Stage 7: Implementation
Finally, create or describe the hierarchy. Avoid boilerplate forced templates.
