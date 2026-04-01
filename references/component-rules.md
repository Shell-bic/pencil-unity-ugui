# Component Rules

Use this file to assist in mapping deduced UI roles into Unity uGUI component stacks.
These are technical implementations guidelines. The exact node naming and hierarchy must come from the Global Structural Reasoning phase, not from this list.

## Core Component Mappings

- **Visual Text**: `Text` or `TextMeshProUGUI` (if requested).
- **Backgrounds & Sliced Panels**: `Image`. Use 9-slice sprites when resizing to avoid warped corners.
- **Complex imported bitmaps / dynamic textures**: `RawImage`. (Only when truly not purely UI Sprites).
- **Interactive hotspots**: `Image` (Alpha = 0) + `Button` or `PointerClickHandler`.
- **Structural Groups**: `RectTransform`. Only add `CanvasGroup` if entire blocks need global alpha fades or wholesale interaction blocking.

## Layout Components

- Use `VerticalLayoutGroup`, `HorizontalLayoutGroup`, or `GridLayoutGroup` ONLY when adapting content that dynamically reflows, repeats data, or requires automated spacing algorithms.
- If elements are statically positioned and meant to stay fixed relative to corners/edges, rely entirely on **Anchors** instead of Layout Groups.

## Interaction Separation

When visual fidelity is paramount, separate the visual layer from the interaction layer:
- The visual node (`Image`) shows the button states.
- The interaction node (`Image` with alpha=0, `Button`) rests above it, sized largely enough to catch sloppy clicks without cropping the visual art.
