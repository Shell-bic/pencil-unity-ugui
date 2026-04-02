# Output Contract

> **This is the authoritative output structure.** When the Output Contract and `engineering-plan-template.md` conflict, this document wins.
>
> **Relationship to engineering-plan-template.md:** The template is an *internal planning scratch pad* for the agent to organize intermediate reasoning. The Output Contract defines the *final deliverable shape* presented to the user. The template feeds into the contract, not the other way around.

Unless the user asks for a specific abbreviated output, your response must follow this structured order to guarantee reasoning precedes hierarchy placement.

## 1. FitAssessment & System Summary
A short paragraph capturing the target constraints and visual scope.

## 2. GlobalStructureSummary (CRITICAL)
Explain your deduction of the overall system architecture. 
Must explicitly state whether this is a state-driven single view, a multi-step flow, a routed multi-page system, or an overlay HUD. Defend your reasoning using visual evidence from the design.
**MUST explicitly state:** The alternative structure rejected + the exact reason why. (e.g., "Not a routed multi-page system because no mutually exclusive view switching was observed.")

## 3. RegionRoleMap
Break down the top-level areas by their semantic purpose in the application. Do not use Unity object names here.
Example: "Navigation Matrix", "Hardware Control Panel", "Data Detail Flyout".

## 4. InteractionModelInference
Describe how user inputs affect the state of the application. Does clicking a button swap a local panel, push a new route history state, or trigger a global event? Define what kind of controller is logically required to manage this.

## 5. HierarchyPlan
Only after the above reasoning should you list the intended Unity tree structure.
Ensure prefixes (`Group_`, `State_`, `Panel_`, `Flow_`) align with your deduced structure.

## 6. AnchorPlan
For major structural parents, list their anchor intent and stretch logic. Keep concise.

## 7. AssetPlan
State which nodes demand `simple-sprite`, `sliced-sprite`, or `hit-area` mappings.

## 8. Component & PrefabBinding Plan
For important nodes, state the Unity component stack and prefab boundaries.
Define where the behavior logic resides (e.g., an Inferred Controller) based on Stage 4. 

## 9. Implementation & Validation Notes
Notes on what should be mutated via Unity Skills vs manual tuning.
Explicitly state: "Which areas or decisions still require manual human confirmation."
