# Prefab and Binding Rules

Use this file when deciding how a Pencil-translated uGUI screen should be decomposed into prefabs, controllers, and route-binding responsibilities.

## Contents

- Principle
- Prefab boundaries
- Script boundaries
- Route binding boundaries
- Recommended runtime roles
- Anti-patterns
- Agent checklist

## Principle

Do not leave the produced screen as one flat hierarchy with behavior scattered across buttons.

The final result should separate:

- reusable visuals
- screen structure
- runtime behavior
- route intent

## Prefab boundaries

Good prefab candidates:

- repeated cards
- pills
- common panels
- shared nav items
- modal shells

Keep local to the screen when:

- the structure is one-off
- the node is tightly tied to a single screen composition
- extracting it would make the hierarchy harder to read

Rules:

- extract when reuse is likely or repetition already exists
- do not prefab every tiny node
- do not leave obviously repeated blocks duplicated by hand

## Script boundaries

Scripts should primarily own:

- state changes
- route requests
- data assignment
- show/hide logic

Scripts should not primarily own:

- hardcoded design geometry for every child
- ad hoc layout compensation
- per-button business logic scattered across unrelated objects

## Route binding boundaries

Route binding should be explicit and centralized.

Prefer:

- a route id or target field on the clickable node
- a router/controller that resolves transitions

Avoid:

- burying navigation logic only inside inspector click lists
- duplicating page transition logic across many button objects

## Recommended runtime roles

Typical split:

- `Screen_*` root
  - screen-level visibility and lifecycle
- reusable `Panel_*` or `Card_*` prefabs
  - visual structure only, plus minimal local state if justified
- `UIRouter`
  - cross-screen navigation
- `UIScreenController`
  - per-screen setup and internal toggles
- route-bearing click nodes
  - emit route intent, do not own transition policy

These names are conventions, not hard requirements, but later agents should preserve the role separation.

## Anti-patterns

- Do not make every node a prefab.
- Do not hardcode all navigation logic separately on each `Button`.
- Do not let screen controllers become giant layout registries.
- Do not duplicate the same card or nav item hierarchy across screens when a prefab would clearly help.

## Agent checklist

Before finalizing structure, ask:

- Which nodes are genuinely reusable?
- Which behavior belongs at screen scope versus element scope?
- Where should route intent live?
- Would this hierarchy still be understandable after three more screens are added?