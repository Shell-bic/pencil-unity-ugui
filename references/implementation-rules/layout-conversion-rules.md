# Layout Conversion Rules

Use this file when translating a Pencil page into a Unity uGUI layout plan. All layout rules here are secondary to the global architectural analysis.

## Contents
- Design canvas assumptions
- Conversion order
- Coordinate translation
- Hierarchy shaping
- Verification checklist

## Design canvas assumptions
Assume Pencil gives you a top-left based canvas. Unity asks for anchors, pivots, and parent-relative offsets.
Layout plans must start with structural relationship (parent/child) and anchor alignment, never raw coordinates.

## Conversion order
Translate in this order:
1. Identify the semantic role of the region (Is it a contextual popup, a status bar, a content block?)
2. Choose the nearest structural parent based on the inferred global architecture.
3. Choose the anchor and pivot intent based on the design's alignment behavior.
4. Decide whether the node is fixed-placement or stretch.
5. Derive the final position and size.

## Coordinate translation
Pencil usually measures from the top-left of the artboard. Unity `RectTransform` placement depends on anchor and pivot.
Practical rule:
- If the node is anchored top-left within its parent, translate Pencil `x` directly and invert `y`.
- If the node is anchored to a centered or stretched parent, mathematically subtract the parent offset before placing it.
- Never use raw root-canvas coordinates for an element that logically belongs inside a sub-panel.

## Hierarchy shaping
Build the tree by visual responsibility based on your global reasoning (e.g. `SystemState`, `ContextualArea`, `ActionGroup`).
Do not group by asset type alone. 

## Verification checklist
Before accepting the layout plan, confirm:
- The hierarchy clearly reflects the semantic inference.
- Anchors match structural intent (e.g., bottom-aligned elements are actually anchored to the bottom).
- Sliced assets are only specified where resizing needs corner preservation.
- The result matches the design visual story without injecting unneeded page-routing overhead.
