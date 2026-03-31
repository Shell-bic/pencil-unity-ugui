# Asset Rules

Use this file when deciding how Pencil visuals should become Unity UI assets.

## Contents

- Principle
- Asset classes
- 9-slice guidance
- Full background guidance
- Text vs image decision
- Import guidance
- Reuse guidance
- Anti-patterns
- Agent checklist

## Principle

Do not treat every visual layer as a plain sprite.

Classify each asset first, then choose the correct Unity representation.

For high-fidelity exhibition UI, many of the most recognizable controls should be implemented as `background cutout art + live text + transparent hit layer` rather than pure color simulation.

## Asset classes

### `simple-sprite`

Use for:

- logos
- icons
- decorative arrows
- fixed background illustrations
- non-stretching ornaments

Unity target:

- `Image`
- `Image Type = Simple`

### `sliced-sprite`

Use for:

- rounded panels
- pills
- bordered cards
- speech bubbles
- container backgrounds reused at multiple sizes

Unity target:

- `Image`
- `Image Type = Sliced`

If corners or borders must survive resizing, prefer `sliced-sprite`.

### `text`

Prefer live text for:

- titles
- labels
- button copy
- metrics
- tabs
- content that may change, localize, or be rebound

Unity target:

- `Text`

Default to built-in `uGUI Text`.

Only recommend `TMP` when:

- the user explicitly asks for it
- the project already uses `TMP` as a hard standard
- text quality, font fallback, or styling requirements clearly justify the extra dependency path

Do not bake editable copy into images unless there is a hard visual requirement.

If the background or pill shape is exported as art for fidelity, keep the caption live whenever the typography itself is not inseparable from the artwork.

### `hit-area`

Use for:

- invisible click targets
- enlarged touch areas
- interactions where the visible art should not own the button state

Unity target:

- `Button`
- optionally with transparent or subtle `Image`

## 9-slice guidance

Use 9-slice when:

- the element has rounded corners
- the border thickness matters
- the asset is reused across multiple widths or heights
- the center should stretch without warping the frame

Avoid `Simple` for rounded reusable panels. It will warp corners.

## Full background guidance

Use a full background sprite when:

- the background is fixed to the screen
- it is not expected to resize independently
- it carries atmosphere or decoration rather than reusable container logic

Do not turn the entire screen into one giant clickable background just because the art is flat.

## Text vs image decision

Prefer text over image when:

- the value may change
- localization is likely
- the text needs better clarity on screen
- accessibility or maintainability matters

Prefer image over text only when:

- the typography is inseparable from the artwork
- the text is treated as a decorative label
- exact visual styling cannot be reproduced reliably with available fonts

## Import guidance

For Unity UI sprites, later agents should verify:

- `Texture Type = Sprite (2D and UI)`
- `Mesh Type = Full Rect`
- `Mip Maps = off` for standard UI sprites
- compression is low enough for UI clarity
- `Border` is configured for sliced sprites

## Reuse guidance

If two visuals share structure and only differ by copy or icon:

- reuse one prefab/component
- swap sprite or text

Do not generate unique one-off structures for obviously repeated cards or pills.

If two controls look related but their cutout art, proportions, or text centering differ enough to be noticeable, keep them as controlled variants instead of forcing one generic visual layout.

## Anti-patterns

- Do not stretch rounded assets as `Simple`.
- Do not bake all text into PNGs by default.
- Do not replace a distinctive hero pill or panel with a flat color block when the cutout art is what carries the fidelity.
- Do not make visual images own the click area when a larger hit target is needed.
- Do not export a giant composite image if the screen should support interaction and page-level maintenance.

## Agent checklist

Before finalizing an asset decision, ask:

- Will this node ever resize?
- Does the border or corner shape matter?
- Should this content stay editable as text?
- Is the click target the same as the visible art, or should it be separate?
