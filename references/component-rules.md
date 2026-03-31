# Component Rules

Use this file when deciding which Unity components should be attached to each node in a Pencil-to-uGUI translation.

## Contents

- Principle
- Core structural components
- Visual components
- Interaction components
- Layout and sizing components
- Masking and scrolling components
- Default component stacks by node type
- Anti-patterns
- Agent checklist

## Principle

Do not attach components opportunistically.

Every important node should have a deliberate component stack based on its role:

- structure
- visual rendering
- interaction
- layout
- state control

If two nodes look similar but have different responsibilities, they should not automatically share the same component stack.

If two controls look similar but differ visibly in proportions, centering, or active-state presentation, they should not automatically share the same visual layout configuration either.

## Core structural components

### `Canvas`

Use for:

- the UI root
- major overlay roots only when a separate canvas is justified

Default root stack:

- `Canvas`
- `CanvasScaler`
- `GraphicRaycaster`

Rules:

- prefer a single main canvas by default
- add nested canvases only for a clear sorting or rebuild reason
- do not treat the existence of a pure UI canvas as a reason to delete `Main Camera` or other default scene infrastructure

### `CanvasScaler`

Use for:

- the root canvas of a screen-based UI

Default:

- `Scale With Screen Size`

### `EventSystem`

Use:

- once per scene

Rules:

- do not create duplicates
- do not add one per screen

### `RectTransform`

Use:

- on every uGUI node

Rules:

- treat it as mandatory structure, not an optional component

## Visual components

### `Image`

Use for:

- backgrounds
- cards
- pills
- icons
- decorative art
- simple button visuals

Prefer:

- `Simple` for fixed non-stretching sprites
- `Sliced` for reusable rounded or bordered visuals

### `RawImage`

Use only when:

- the source is a `Texture`, render target, camera feed, or video-like content

Do not use `RawImage` for normal sprite-based UI art.

### `Text`

Use for:

- editable labels
- titles
- tabs
- values
- button captions

Default:

- built-in `uGUI Text`

Only upgrade to `TMP` when the user explicitly asks for it or the project already requires it.

### `Shadow` / `Outline`

Use sparingly for:

- simple emphasis on text or icons

Rules:

- prefer art-driven styling first
- avoid stacking multiple outline/shadow effects unless clearly justified

## Interaction components

### `Button`

Use for:

- clickable actions
- navigation hotspots
- cards that behave like buttons

Rules:

- separate click area from purely decorative art when needed
- for fidelity-first controls, prefer a transparent `Button` layer above the visual art instead of making the art node itself own interaction
- do not put `Button` on every image just because it is visible

### `Selectable` family

Use:

- `Button`, `Toggle`, `Slider`, `Scrollbar`, `Dropdown` only when the interaction type truly matches

Rules:

- do not model navigation cards as `Toggle` unless mutually exclusive state is required
- do not use `Slider` for progress display unless the user needs interaction

### `CanvasGroup`

Use for:

- show/hide groups
- fading groups
- temporarily blocking interaction

Prefer `CanvasGroup` when a whole region needs unified alpha or interactivity control.

## Layout and sizing components

### `HorizontalLayoutGroup` / `VerticalLayoutGroup` / `GridLayoutGroup`

Use only when:

- children repeat in a regular flow
- spacing is a true layout concern

Do not use them for fixed exhibition compositions that are better expressed through anchors and manual placement.

### `LayoutElement`

Use for:

- controlling preferred size inside a layout group
- overriding flexible sizing in repeated structures

### `ContentSizeFitter`

Use carefully for:

- text wrappers
- fit-to-content subtrees with small scope

Rules:

- avoid broad use on complex parent chains
- avoid combining carelessly with layout groups on the same node

### `AspectRatioFitter`

Use only when:

- an element must preserve an explicit aspect ratio

Do not use it to compensate for bad anchor or size decisions.

## Masking and scrolling components

### `Mask`

Use when:

- you need alpha-based masking
- the visual shape matters

### `RectMask2D`

Prefer when:

- rectangular clipping is enough
- performance and simplicity matter

### `ScrollRect`

Use only when:

- the design really calls for scrollable content

Do not add scrolling to a fixed dashboard just because content feels dense.

## Default component stacks by node type

### `screen-root`

- `RectTransform`
- optionally `CanvasGroup` for page visibility control

### `region`

- `RectTransform`
- optionally `CanvasGroup` if the whole region needs state control

### `panel`

- `RectTransform`
- `Image`

### `image`

- `RectTransform`
- `Image`

### `text`

- `RectTransform`
- `Text`

### `hit-area`

- `RectTransform`
- `Image` if a raycast target is needed
- `Button`

### `nav-control`

- `RectTransform`
- visual component as needed
- `Button`
- optional route-binding script in project code

### `scroll-region`

- `RectTransform`
- `Image` if visual background is needed
- `RectMask2D` or `Mask`
- `ScrollRect`

## Anti-patterns

- Do not use `RawImage` for normal sprites.
- Do not add `Button` to decorative images by default.
- Do not force visually distinct primary controls into one identical prefab layout too early.
- Do not add layout groups to fixed-position compositions unless there is true repeated structure.
- Do not stack `ContentSizeFitter` and layout groups carelessly.
- Do not create multiple `EventSystem` objects.
- Do not create nested canvases without a concrete reason.

## Agent checklist

Before finalizing a node, ask:

- Is this node structural, visual, interactive, or stateful?
- Which component is actually rendering the content?
- Does the node need interaction, or only a sibling hit-area?
- Is a layout component justified, or is fixed placement clearer?
- Would this component choice still make sense after the screen grows?
