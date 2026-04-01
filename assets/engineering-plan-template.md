# uGUI Structural Plan Template

Use this format when outputting a plan. Replace brackets with deduced values based on the initial system reasoning.

## Fit Assessment
[Brief summary of whether uGUI is appropriate and any major constraints discovered]

## Global Structure Summary
[CRITICAL: Describe the foundational architecture deduced from the design. Is it a state machine, an overlay HUD, a linear workflow, or a routed multi-page app? Do not assume page-routing.]

## Region Role Map
[Map the top-level semantic areas without assuming Unity hierarchy types yet]
- [Semantic Area 1]: [Role/Purpose]
- [Semantic Area 2]: [Role/Purpose]

## Interaction Model Inference
[How do inputs change the system? Do they toggle local filters, swap states, or trigger full router navigation?]

## Hierarchy Plan
[Design the Unity tree based on the deduced architecture. Use neutral prefixes like Group_, State_, Flow_, Panel_ unless Screen_ is specifically justified.]

- `[Root_Node]` (e.g., Canvas_Main or WorldCanvas_Target)
  - `[Inferred_Structural_Node_1]`
    - `[Child_Panel]`
    - `[Text/Image]`
  - `[Inferred_Structural_Node_2]`

## Anchor Plan
- `[Important Node A]`: Parent = `[Parent]`, Anchor = `[Preset]`, Intent = `[Fixed/Stretch]`
- `[Important Node B]`: Parent = `[Parent]`, Anchor = `[Preset]`, Intent = `[Fixed/Stretch]`

## Asset Plan
- `[Visual Node 1]`: [simple-sprite / sliced-sprite / text / hit-area]

## Component & Prefab Binding Plan
- `[Structural Group Node]`: `RectTransform`, `[CanvasGroup?]`
  - Controller Intent: `[Inferred Controller Role, e.g. StateGroupController, FlowDirector]`
- `[Interactive Node]`: `RectTransform`, `[Button]`

## Navigation & Intent Plan
[Only include if interactions explicitly drive structural jumps]
- [Source Node] -> [Inferred Route Target or State Mutation]

## Validation Checklist
- [ ] Structural deduction is explicitly answered (HUD vs Flow vs Page routed)
- [ ] Hierarchy perfectly reflects the semantic structural deduction
- [ ] Anchor intent verifies structural dependencies
- [ ] Asset plan balances simple vs sliced sprites
- [ ] Prefab boundaries and inferred controllers are explicitly listed
