# Anchor Rules

Use this file when deciding how a Pencil node should map to `RectTransform` anchors and positioning.

## Contents

- Principle
- Parent-first rule
- Recommended presets
- Fixed-placement vs stretch
- Pivot guidance
- Anti-patterns
- Agent checklist

## Principle

Anchors express structural intent, not just coordinates.

Choose anchors based on which edge or region the element conceptually belongs to. Do not default everything to `MiddleCenter`.

When converting from Pencil, treat the source as a top-left design canvas first. Choose the parent, anchor, and structural region before translating coordinates into Unity space.

## Parent-first rule

Always choose the parent container first.

- `Canvas` is the global root
- `Screen_*` is the per-page root
- `Region_*` is a structural grouping
- child nodes should usually anchor against a `Region_*` or `Panel_*`, not directly against `Canvas`

If many children are anchored directly to the root, the hierarchy is probably too flat.

If a node is visually part of a shell edge, prefer anchoring it to that shell region instead of compensating from the Canvas root with a large offset.

## Recommended presets

### `StretchAll`

Use for:

- full-screen backgrounds
- screen root wrappers
- large content panels with stable margins
- overlays that should fill the parent

Prefer this for:

- `Bg_Full`
- `Screen_*`
- `Panel_Content` when it is bounded by left/right/top/bottom offsets

### `TopLeft`

Use for:

- logos
- left navigation columns
- fixed pills or cards near the top-left
- fixed-position labels in large-screen compositions

This is the safest default for fixed-screen exhibition layouts.

### `TopRight`

Use for:

- language toggles
- status widgets
- utility buttons in the upper-right

### `BottomLeft` / `BottomRight`

Use for:

- footer controls
- bottom-edge badges
- bottom-corner actions

### `MiddleCenter`

Use for:

- truly centered hero/title blocks
- modal dialogs
- centered status or loading overlays

Do not use `MiddleCenter` for elements that conceptually belong to an edge or region.

### `StretchHorizontal`

Use for:

- top bars
- bottom bars
- separators or tracks that should stretch horizontally

### `StretchVertical`

Use for:

- left or right side rails
- decorative vertical bands
- sidebars intended to scale in height with the screen

## Fixed-placement vs stretch

Use `fixed-placement` when:

- the element is part of a static composition
- width and height should remain fixed
- the design resembles poster placement

Use `stretch` when:

- the element is a region or container
- the element should adapt to the parent bounds
- the design intent is edge-bounded, not point-placed

## Pivot guidance

Use pivots that match the anchor and editing intent:

- `TopLeft` anchor -> pivot usually `(0, 1)`
- `TopRight` anchor -> pivot usually `(1, 1)`
- `BottomLeft` anchor -> pivot usually `(0, 0)`
- `MiddleCenter` anchor -> pivot usually `(0.5, 0.5)`
- stretched containers -> pivot is less important, default values are acceptable unless animation/editing requires otherwise

If a node is meant to stay visually fixed but the position still feels off, re-check whether the pivot matches the intended edge before changing coordinates.

## Anti-patterns

- Do not anchor everything to the center and then compensate with large coordinates.
- Do not stretch a node if its content is supposed to stay visually fixed.
- Do not use a layout group under a parent whose children also depend on fixed anchor offsets.
- Do not anchor decorative children against `Canvas` if they belong to a panel.

## Agent checklist

Before finalizing anchors, confirm:

- What is the nearest structural parent?
- Is this node edge-bound or point-placed?
- Should it resize with the parent or remain fixed?
- Does the chosen anchor make later maintenance easier?
