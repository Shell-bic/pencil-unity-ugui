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

## Hierarchy naming

Prefer stable prefixes:

- `Canvas_*`
- `Screen_*`
- `Region_*`
- `Panel_*`
- `Card_*`
- `Img_*`
- `Txt_*`
- `Btn_*`
- `Hit_*`

Rules:

- use the same prefix set across the whole screen set
- prefer semantic names such as `Region_LeftNav` over raw coordinate names like `LeftBox42`
- keep display text out of node names unless it is truly the identity of the node

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

Prefer:

- `UIScreenController`
- `HomeScreenController`
- `UIRouter`
- `NavButtonRouteBinder`

Rules:

- scripts should be named by responsibility, not by design appearance
- screen controllers should use screen-scoped names
- cross-screen systems should use global names

## Route naming

Prefer stable route ids or names such as:

- `Home`
- `Overview`
- `Detail`
- `Settings`

Rules:

- route ids should be short and stable
- do not derive route ids from temporary art labels
- route names should not depend on hierarchy depth

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

## Agent checklist

Before finalizing names, ask:

- Does this name describe role or just location?
- Will this still make sense after three more screens are added?
- Is this naming convention consistent with the rest of the hierarchy?
- Could a different agent infer behavior from this name alone?
