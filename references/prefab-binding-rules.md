# Prefab and Binding Rules

Use this file when deciding how a screen or hierarchy should be decomposed into prefabs and controllers. 
**Crucially, do not default to `UIRouter` or `UIScreenController` unless the system has been explicitly identified as a multi-screen routed application.**

## Contents
- Principle
- Prefab boundaries
- Script boundaries
- Inferred Runtime Roles
- Anti-patterns

## Principle
Separate reusable visuals, structural hierarchy, and runtime behavior. However, the exact boundaries must emerge from the specific design's interaction model, not a one-size-fits-all template.

## Prefab boundaries
Extract as prefabs when:
- Visual clustering is repeated (e.g., identical cards, standardized buttons).
- A monolithic overlay is needed globally (e.g., a universal confirmation modal).
Keep local when:
- The structure is highly unique to the current contextual flow.

## Script boundaries
Scripts should own state machines, data assignment, and interaction triggers.
Avoid writing scripts that perform ad hoc, hardcoded layout compensations—use RectTransforms and Anchors instead.

## Inferred Runtime Roles
Instead of forcing a `UIScreenController`, deduce the actual controller category needed:

- **StateGroupController**: For single-view applications swapping localized states (e.g., changing tabs or expanding filters).
- **FlowDirector**: For multi-step sequences where A goes to B goes to C (e.g., an onboarding wizard).
- **OverlayManager**: For global HUDs and interruptive popups.
- **RouteResolver / PageController**: ONLY when a true multi-page architectural context exists.

These neutral names encourage you to think about what the script *does*, rather than defaulting to "Screen" logic.

## Anti-patterns
- **The Router Bias**: Do not assume every button changes the entire screen. Many buttons just mutate local panel data.
- **The Central Monolith**: Do not let a single controller become a giant registry for 50 child components if the UI clearly consists of distinct, autonomous widget panels.
- Do not make every visual node a prefab just for the sake of it.