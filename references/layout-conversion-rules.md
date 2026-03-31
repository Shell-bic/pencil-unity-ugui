# Layout Conversion Rules

Use this file when translating a Pencil page into a Unity uGUI layout plan.

## Contents

- Design canvas assumptions
- Conversion order
- Shell-first mapping
- Coordinate translation
- Hierarchy shaping
- When a page feels messy
- Verification checklist

## Design canvas assumptions

Assume Pencil gives you a top-left based canvas. Unity asks for anchors, pivots, and parent-relative offsets.

That means the layout plan should not start with raw coordinates. It should start with:

- what the structural parent is
- whether the node is shell, region, content, or hotspot
- which edge or region the node belongs to

## Conversion order

Translate in this order:

1. identify the page or region role
2. choose the nearest structural parent
3. choose the anchor and pivot intent
4. decide whether the node is fixed-placement or stretch
5. derive the final position and size

Do not reverse the order.

## Shell-first mapping

For fixed-screen exhibition layouts, most pages should map into:

- `Shell_Background`
- `Shell_Header`
- `Shell_LeftNav`
- `Shell_ContentPanel`
- `Shell_RightRail`

Only after the shell is stable should the page-local content be placed.

This avoids the common mistake of treating edge-bound controls like centered content.

## Coordinate translation

Pencil usually measures from the top-left of the artboard.
Unity `RectTransform` placement depends on anchor and pivot.

Practical rule:

- if the node is anchored top-left within its parent, translate Pencil `x` directly and invert `y`
- if the node is anchored to a centered or stretched parent, subtract the parent offset before placing it
- if the node belongs to an edge region, calculate relative to that region, not to `Canvas`

Use raw coordinates only after the anchor choice is settled.

## Hierarchy shaping

Build the tree by visual responsibility:

- shell
- region
- panel
- local content
- hotspot

Do not group by asset type alone.

If the result feels flat, the likely fix is a missing shell region or an incorrectly centered node, not another script.

## When a page feels messy

Before changing positions, ask:

- Is the page missing a shell region?
- Was an edge element anchored as a center element?
- Did a repeated control get treated as a one-off asset?
- Did a background or panel get placed at the wrong hierarchy level?

Those questions often reveal the real issue faster than coordinate tweaking.

## Verification checklist

Before accepting the layout plan, confirm:

- the shell regions are visible in the hierarchy
- anchors match structural intent
- edge-bound nodes are not centered by accident
- repeated controls are consistent in size and rhythm
- text remains live where editing matters
- sliced assets are only used where resizing needs corner preservation
- the hierarchy still matches the design's visual story
