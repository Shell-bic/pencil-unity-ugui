---
name: pencil-unity-ugui
description: Translate Pencil MCP designs or structured layout specs into Unity uGUI plans or implementations. Use when the task combines Pencil/design analysis with Canvas, RectTransform, anchors, sliced sprites, hotspot navigation, or fixed-screen dashboard and exhibition UI production. Prefer general Unity UI skills for pure uGUI authoring that does not involve Pencil or design translation. Do not use for UI Toolkit unless the user explicitly asks for comparison or migration.
metadata:
  short-description: Translate Pencil designs into Unity uGUI with anchor, slicing, and navigation rules
---

# Pencil Unity uGUI

This is a `design-translation` skill, not a general-purpose `uGUI` authoring skill.

If the user only wants to hand-build or tweak `Canvas/Button/Text/Image` without a Pencil or design-translation angle, prefer the general Unity UI skills instead of this skill.

Use this skill when the target output is `Unity uGUI`, and the source of truth is either:

- a `Pencil MCP` design
- a screenshot/layout spec that should be normalized through Pencil-like structure
- a fixed-screen composition that needs `Canvas + RectTransform + Image + Text + Button`

This skill is intentionally focused on `uGUI`. It exists to keep later agents from mixing:

- `uGUI`
- `UI Toolkit`
- browser layout mental models
- generic scene building unrelated to Canvas UI

## Non-goals

Treat these as exclusions unless the user explicitly asks for comparison:

- Do not use this skill for `UI Toolkit`, `UXML`, `USS`, or `UIDocument`
- Do not describe `RectTransform` as if it were browser `Flexbox`
- Do not assume a fixed-screen exhibition layout should become a responsive app layout
- Do not convert every design grouping into a `LayoutGroup`
- Do not claim pixel-perfect parity without screenshot-based verification

If the task is ambiguous, read [references/anti-patterns.md](references/anti-patterns.md) before generating output.

## Tool split

Use `Pencil MCP` for:

- reading the design structure
- inspecting screenshots, bounds, spacing, and grouping
- finding repeated panels/cards/tiles
- classifying nodes as background, panel, text, decoration, or hotspot
- verifying whether the produced hierarchy still matches the design intent

Use `Unity Skills` for:

- creating `Canvas`, panels, images, buttons, text, and containers
- setting anchors and `RectTransform` values
- arranging children only when a real layout group is justified
- creating the screen hierarchy and naming
- scaffolding navigation or interaction wiring

This skill is responsible for deciding when each tool should be used, in which order, and with which constraints.

## Default stance

Assume the user wants one of two outcomes:

- `Plan only`: analyze the design and output a production plan
- `Implement in Unity`: directly create or modify the `uGUI` hierarchy with `Unity Skills`

Default to `plan only` unless the user explicitly asks to modify Unity.

Do not switch to direct editor mutation implicitly.
Do not attempt Unity UI creation in `semi-auto`.

## Best-fit use cases

This skill is a strong fit for:

- exhibition or control-room screens
- dashboards on fixed resolutions
- information kiosks
- page-based touchscreen UIs
- image-heavy layouts with a few text and button hotspots
- screen-to-screen navigation

This skill is a weaker fit for:

- highly responsive product UIs
- dynamic feeds with many adaptive states
- long virtualized data lists as the dominant use case
- interfaces that rely on `UI Toolkit` styling or DOM-like flows

When the fit is weak, say so explicitly and explain why.

## Workflow

1. Confirm the target is really `uGUI`.
2. Classify the task:
   - planning only
   - implementation
   - review / refactor
   - migration from another UI system
3. Inspect the design with `Pencil MCP` before creating Unity nodes.
4. If the file appears to contain multiple related pages, scan the whole document before planning a single page:
   - identify global shell regions reused across pages
   - identify page families or templates
   - identify repeated controls that should become prefabs
   - separate true pages from loose asset boards, reference art, or scratch areas
5. Classify the screen type:
   - full-screen fixed composition
   - panel-based screen
   - list/grid screen
   - popup/dialog
   - overlay/HUD
6. If the design is a multi-page fixed-screen system, extract the shared shell before deep page planning:
   - `Shell_LeftNav`
   - `Shell_TopBar`
   - `Shell_ContentPanel`
   - `Shell_BottomBar`
   - `Shell_RightRail`
7. If the user is primarily judging visual fidelity, pick the current selected page as the visual baseline page before broadening to the rest of the system.
8. Classify important nodes using the rules in [references/workflow-checklist.md](references/workflow-checklist.md).
9. Decide layout mode per parent:
   - `fixed-placement`
   - `layout-group`
10. Decide anchors before creating the hierarchy. Use [references/anchor-rules.md](references/anchor-rules.md).
11. Decide asset strategy before creating nodes. Use [references/asset-rules.md](references/asset-rules.md).
12. Choose the Unity component stack for important nodes. Use [references/component-rules.md](references/component-rules.md).
13. Decide typography and visual-effect rules. Use [references/typography-visual-rules.md](references/typography-visual-rules.md).
14. Decide prefab, script, and route-binding boundaries. Use [references/prefab-binding-rules.md](references/prefab-binding-rules.md).
15. Decide naming conventions. Use [references/naming-rules.md](references/naming-rules.md).
16. Decide content and data-binding rules. Use [references/data-binding-rules.md](references/data-binding-rules.md).
17. Create or describe navigation last.
18. Format the answer using [references/output-contract.md](references/output-contract.md).

## Generation rules

- Prefer region-based hierarchy over a flat Canvas.
- Prefer built-in `uGUI Text` for text by default.
- Only switch to `TMP` if the user explicitly requests it or the project already standardizes on `TMP`.
- When visual fidelity matters more than edit-time convenience, prefer `background cutout art + live text + separate transparent hit layer` for hero panels, navigation pills, and primary action controls.
- Children should be positioned relative to the nearest structural parent, not always the Canvas root.
- For multi-page systems, plan the shared shell and page families before detailing a single target page.
- Use `fixed-placement` for large-screen fixed compositions.
- Use `LayoutGroup` only when spacing is intentionally regular and repeatable.
- Separate visual nodes from click targets when that improves maintainability.
- For large-screen touch UIs, default to a separate `Hit_*` layer for navigation, tabs, media controls, and toggle-like blocks unless the visual node clearly needs to own the button feedback.
- Use explicit names like `Screen_*`, `Region_*`, `Panel_*`, `Card_*`, `Img_*`, `Txt_*`, `Btn_*`, `Hit_*`.
- Use `9-slice` for reusable rounded panels, pills, and bordered containers.
- Do not over-generalize similar-looking controls into one rigid prefab layout if their proportions, text centering, or active states visibly differ in the design.
- Read [references/layout-conversion-rules.md](references/layout-conversion-rules.md) when you need to justify how a Pencil page becomes a Unity hierarchy.
- Translate Pencil coordinates from the page's top-left coordinate system into Unity's anchor/pivot system before judging position. Prefer to decide parent, anchor, and structural region first, then derive coordinates from that mapping.
- Treat cross-page repetition as a component/region clue, not as proof that two nodes should share one exact size or one exact layout recipe.
- When a page feels visually "busy" or "flat," first check whether the hierarchy is missing shell regions or whether an edge-bound element was accidentally treated like a centered element.
- Keep navigation intent separate from visual styling.
- When route targets are not explicit in the design, record clickable elements as candidate hotspots or static controls instead of inventing route mappings.
- Use a small, named typography scale instead of arbitrary per-node font sizes.
- Prefer art-driven or sliced visual styling over piling on multiple effect components.
- Keep prefab boundaries, binding scripts, and visual hierarchy separate.
- Keep screen, prefab, script, and route naming stable and role-driven.
- Default to static content assignment unless a live data source or runtime binding need is explicit.
- Prefer explicit, readable binding paths over hidden implicit wiring.

## Unity Skills usage rules

When implementation is requested:

- Before direct Unity mutation, load and follow the `unity-skills` and `unity-ui` skill rules.
- Treat `Unity Skills` UI creation as `full-auto` work only.
- If the user has not explicitly asked to create or modify Unity UI in the editor, stay in planning mode.
- Prefer `ui_create_batch` for 2 or more sibling elements.
- Use `ui_set_anchor` before fine-tuning position with `ui_set_rect`.
- Use `ui_layout_children` only for real repeated flows.
- Use `ui_set_image` and `component_set_property` for sprite and image configuration.
- Keep the number of root Canvas children small and structurally meaningful.
- For multi-step editor mutation, prefer a workflow wrapper so the build remains reversible and traceable.
- Do not delete `Main Camera`, `Directional Light`, or `Global Volume` by default in a fresh Unity scene unless they clearly interfere with the requested result or the user explicitly asks for a pure-UI scene.
- When fidelity is the primary goal, build and verify the currently selected page first as a visual baseline before scaling the shared shell to the rest of the system.
- After any domain reload or asset import burst, verify `Unity Skills` is healthy again before concluding that editor automation failed.

If a layout can be expressed by a region container plus fixed child placement, prefer that over forcing a layout group.

## Files to read when needed

- Before direct implementation, load the `unity-skills` and `unity-ui` skills and follow their mode requirements.
- For trigger calibration and borderline examples: [references/trigger-examples.md](references/trigger-examples.md)
- For anchor selection and `RectTransform` strategy: [references/anchor-rules.md](references/anchor-rules.md)
- For a short homepage-specific placement checklist: [references/homepage-layout-checklist.md](references/homepage-layout-checklist.md)
- For slicing, sprite import, and text-vs-image decisions: [references/asset-rules.md](references/asset-rules.md)
- For Unity component selection and default stacks: [references/component-rules.md](references/component-rules.md)
- For typography hierarchy and allowed visual effects: [references/typography-visual-rules.md](references/typography-visual-rules.md)
- For prefab boundaries, controller responsibilities, and route binding: [references/prefab-binding-rules.md](references/prefab-binding-rules.md)
- For naming conventions across screens, prefabs, scripts, and routes: [references/naming-rules.md](references/naming-rules.md)
- For content assignment and runtime binding strategy: [references/data-binding-rules.md](references/data-binding-rules.md)
- For the end-to-end execution checklist: [references/workflow-checklist.md](references/workflow-checklist.md)
- For known bad patterns and false equivalences: [references/anti-patterns.md](references/anti-patterns.md)
- For required answer shape: [references/output-contract.md](references/output-contract.md)
- For reusable planning skeletons: `assets/ugui-screen-plan-template.md`, `assets/route-map-template.yaml`, and `assets/prefab-binding-template.yaml`

## Output expectations

When planning or reviewing a uGUI screen, usually provide:

- a short fit assessment
- a hierarchy plan
- an anchor plan
- an asset slicing plan
- a navigation plan
- a verification checklist

When implementing, also provide:

- what was created or changed
- what still needs manual adjustment
- what was verified

If code or Unity mutation is requested, do not stop at explanation. Produce the hierarchy, scripts, or editor actions that are actually needed.
