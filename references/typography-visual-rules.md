# Typography and Visual Rules

Use this file when deciding how text hierarchy and simple visual effects should be standardized in a Pencil-to-uGUI workflow.

## Contents

- Principle
- Typography hierarchy
- Text component defaults
- Visual effect rules
- Color and art rules
- Anti-patterns
- Agent checklist

## Principle

Typography and visual effects should be system-driven, not improvised per node.

Do not recreate a design by scattering arbitrary font sizes, colors, outlines, and shadows across unrelated nodes.

## Typography hierarchy

Prefer a small named scale, for example:

- `Display`
- `Title`
- `Body`
- `Caption`

For each screen, later agents should map major text nodes into one of these tiers before finalizing size and styling.

Rules:

- repeated text roles should share the same style tier
- decorative one-off text still needs a known tier before exceptions are applied
- avoid inventing a new font size for every label

## Text component defaults

Default text path:

- built-in `uGUI Text`

Prefer these defaults unless the design clearly requires something else:

- explicit alignment
- explicit line spacing
- explicit overflow intent
- no blind use of `Best Fit`

Use `Best Fit` only when:

- the design explicitly tolerates scaling text down
- a bounded label needs last-resort fit behavior

Do not use `Best Fit` as a substitute for missing layout or typography decisions.

## Visual effect rules

Allowed simple effects:

- `Shadow`
- `Outline`
- alpha fading through `CanvasGroup`

Rules:

- prefer one effect layer over stacked effect chains
- prefer art assets for complex glows, bevels, or branded lighting treatments
- do not simulate complex graphic design with multiple nested outline/shadow hacks

## Color and art rules

Prefer:

- sprite art for complex frames and badges
- sliced assets for reusable styled containers
- text color changes for semantic emphasis

Avoid:

- using effect components to fake art that should be part of the asset
- mixing too many slightly different text colors for similar roles

## Anti-patterns

- Do not use a unique font size for every node.
- Do not rely on `Best Fit` everywhere.
- Do not stack multiple `Outline` and `Shadow` effects to imitate complex art.
- Do not encode typography hierarchy only through manual inspector tweaking with no named tiers.

## Agent checklist

Before finalizing text and visual styling, ask:

- What is the text role: display, title, body, or caption?
- Is this node following an existing tier or inventing a new one?
- Should the styling be text-driven, asset-driven, or effect-driven?
- Is an effect component actually needed, or should the look come from art?