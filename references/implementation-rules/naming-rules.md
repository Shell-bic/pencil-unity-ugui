# Naming Rules

Use this file when deciding how screens, regions, prefabs, scripts, routes, and content nodes should be named in a Pencil-to-uGUI workflow.

## Contents

- Principle
- Hierarchy naming
- Prefab naming
- Script naming
- Route naming
- Asset and binding key naming
- Anti-patterns
- Agent checklist

## Principle

Names should communicate role first and appearance second.

The purpose of a name is to make the hierarchy understandable after the screen grows, not merely to mirror a design layer label.

> If a name implies a runtime structure that has not been proven in Stage 1–3, that name is invalid.

## Hierarchy naming

### Universal prefixes (always available)

- `Canvas_*`
- `Region_*`
- `Panel_*`
- `Card_*`
- `Img_*`
- `Txt_*`
- `Btn_*`
- `Hit_*`

### Conditional prefixes (require structural proof)

- `Screen_*` — only when Stage 1 explicitly confirms a routed multi-page architecture
- `Shell_*` — only when Stage 2 confirms persistent regions shared across multiple views
- `State_*` — for state-driven single-view systems
- `Flow_*` — for multi-step sequential flows
- `Group_*` — for general structural grouping when no stronger semantic applies

> **GATE:** If Stage 1 has not been completed, do not use `Screen_*` or `Shell_*`. Default to `Region_*` / `Panel_*` / `Group_*`.

Rules:

- use the same prefix set across the whole screen set
- prefer semantic names such as `Region_LeftNav` over raw coordinate names like `LeftBox42`
- keep display text out of node names unless it is truly the identity of the node
- prefix choice must align with the inferred system type from Stage 1-2, not with visual appearance

## Prefab naming

Prefer:

- `Card_Primary`
- `Panel_Info`
- `NavItem_Main`
- `Modal_Base`

Rules:

- prefab names should describe reusable role
- avoid screen-local coordinates in prefab names
- do not create multiple near-duplicate prefab names for the same pattern

## Script naming

Script names are **inferred from the system type**, not picked from a default menu.

### For state-driven single-view systems (inferred)

- `StateGroupController`
- `PanelToggleController`
- `FilterStateManager`

### For multi-step flow systems (inferred)

- `FlowDirector`
- `StepSequenceController`

### For overlay / HUD systems (inferred)

- `OverlayManager`
- `HudController`

### For routed multi-page systems ONLY (requires Stage 1 proof)

- `UIRouter`
- `UIScreenController`
- `PageController`
- `NavButtonRouteBinder`

> **GATE:** `UIScreenController`, `UIRouter`, and `PageController` are **forbidden** unless Stage 1 explicitly confirmed a routed multi-page architecture. Using them without proof is a skill failure condition.

Rules:

- scripts should be named by responsibility, not by design appearance
- the controller category must match the inferred interaction model from Stage 3
- do not default to `Screen` or `Router` naming when simpler state/panel controllers suffice

## Route naming

> **PREREQUISITE:** Route naming only applies when Stage 1 confirmed a routed multi-page architecture. If the system is state-driven, flow-based, or overlay-based, this section does not apply.

Prefer stable route ids or names such as:

- `Home`
- `Overview`
- `Detail`
- `Settings`

Rules:

- route ids should be short and stable
- do not derive route ids from temporary art labels
- route names should not depend on hierarchy depth
- do not introduce route concepts into non-routed systems

## Asset and binding key naming

Prefer:

- `title`
- `subtitle`
- `hero_image`
- `primary_value`

Rules:

- content keys should be data-oriented, not layout-oriented
- avoid names like `left_text_1` unless there is no stronger semantic meaning
- if the same key appears on multiple screens, keep semantics consistent

## Anti-patterns

- Do not leave raw import layer names as final hierarchy names.
- Do not use coordinate-driven names as the main naming scheme.
- Do not let route ids depend on screen object names.
- Do not mix multiple naming conventions in one screen family.
- **Do not use `Screen_*` / `UIRouter` / `UIScreenController` naming unless a routed multi-page architecture was explicitly proven in Stage 1.** This is the single most common naming error.

## Agent checklist

Before finalizing names, ask:

- Does this name describe role or just location?
- Will this still make sense after three more screens are added?
- Is this naming convention consistent with the rest of the hierarchy?
- Could a different agent infer behavior from this name alone?
