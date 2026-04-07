# Unity UI Engineering Plan

> **Role:** This template is an *internal planning scratch pad* used during Stages 1-4 to organize intermediate reasoning. It is NOT the final output format.
>
> **Final output** must follow `references/core-method/output-contract.md`. When this template and the Output Contract conflict on structure or naming, the Output Contract is authoritative.

## 1. System Inference
- Structure type (inferred, not labeled)
- Reasoning
- **Required:** At least one rejected alternative + reason

## 2. Global Structure
- Persistent regions
- Switched regions
- Overlay regions
- Global states
- **Required:** Every region listed must link back to visual evidence

## 3. Region Role Map
- Region_A: role
- Region_B: role
- **Required:** No major visual area may remain unlabeled

## 4. Engineering Architecture Decision
- Why use pages / panels / overlays / flow / mixed structure?
- Alternatives rejected and why
- **Required:** Decision must reference the system type from §1

## 5. Reusable Components
- Component name
- Responsibility
- Reuse scope
- **Required:** Interaction semantics verified for each shared component

## 5.5 Page Truth & Shared Component Facts
- Referenced page -> active primary item
- Referenced page -> secondary navigation shown/hidden
- Referenced page -> selected secondary item
- Shared component family -> exact current Pencil geometry
- **Required:** Shared shell sizing must come from current Pencil facts, not historical Unity screenshots

## 6. Layout & Asset Placement Plan
- Parent ownership
- Anchor strategy
- Asset grouping
- **Required:** No major region may lack parent ownership or anchor intent

## 7. Runtime Behavior
- Navigation / state change / popup / flow / language / media
- **Required:** Controller names must match inferred system type, not defaults

## 8. Implementation Notes
- What should be built first
- What remains for manual refinement
- **Required:** At least one uncertainty or manual-confirmation item listed
