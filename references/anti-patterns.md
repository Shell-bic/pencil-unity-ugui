# Anti-Patterns

Use this file when reviewing a proposed uGUI plan. If the plan matches these anti-patterns, redo it.

## CRITICAL METHODOLOGY ANTI-PATTERNS

- **Skipping Structural Inference**: Do NOT start creating `Screen_` or assigning anchors without explicit reasoning about the global system architecture first.
- **Visual Similarity = Structural Equivalence**: Just because two buttons look identical does not mean they map to the same type of runtime controller. Do not map pure visual patterns directly into structural components before verifying behavior.
- **The Router Bias**: Assuming every UI needs cross-screen routing.

## uGUI ANTI-PATTERNS

- **Center-anchor everything**: Leaving all elements anchored to the center `(0.5, 0.5)` and moving them by hundreds of pixels. Elements must anchor to their logical parent edge or structural container.
- **Everything is a LayoutGroup**: Adding a `HorizontalLayoutGroup` to a panel that only contains two fixed objects at opposite ends. Use manual anchors and fixed placement unless the content actually repeats or reflows.
- **Flatten hierarchy**: Putting 50 images and texts directly under the root Canvas without logical grouping, making the inspector impossible to read.
- **Bake all text into images**: Stripping out editability because a font isn't standard. Unless the font is heavily stylized pixel art, use Unity UI `Text` or `TMP`.
- **Shrinking hit targets**: Keeping the interactive click box exactly the size of a tiny 16x16 icon instead of wrapping it in a generous 48x48 transparent hit area for touch/mouse ease.
