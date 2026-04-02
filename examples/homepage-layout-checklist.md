# Homepage Layout Checklist

> [!CAUTION]
> **PREREQUISITE:** This checklist is only valid when:
> 1. Stage 1 (Global System Analysis) has been completed
> 2. Stage 2 (Engineering Architecture Planning) confirmed a **persistent-shell architecture** with shared structural regions
> 3. The RegionRoleMap explicitly identifies persistent regions that survive across views
>
> If these prerequisites are not met, **do not use this checklist**. Use the general workflow-checklist.md pipeline instead.
>
> This is an **example for a specific architecture type**, not a default starting template.

Use this checklist when turning a Pencil fixed-screen homepage into Unity uGUI, **after structural reasoning confirms a shell-based layout**.

## 1. Start with structural regions

Create the structural regions based on your Stage 2 RegionRoleMap:

- `Region_Background` (or `Shell_Background` if persistent-shell was confirmed)
- `Region_Header`
- `Region_LeftNav`
- `Region_ContentPanel`
- `Region_RightRail`

> **Note:** Use `Shell_*` prefix only if Stage 2 confirmed these regions persist across multiple views. For single-view systems, prefer `Region_*` or `Group_*`.

If the hierarchy does not have these regions, do not start placing detailed controls yet.

## 2. Decide what is edge-bound

Before positioning, ask whether each node belongs to:

- top-left
- top-right
- left rail
- right rail
- center content

Do not let an edge-bound node drift into a centered placement.

## 3. Convert coordinates through the parent

Do not place everything from `Canvas`.

Instead:

- choose the nearest structural parent
- choose the anchor preset that matches the node's role
- then derive the `RectTransform` offset from that parent

If a control looks wrong, re-check the parent before changing the raw coordinates.

## 4. Keep repeated controls consistent

Repeated controls should share:

- same visual family
- same corner treatment
- same text alignment intent
- same hit-area policy

They do not have to share the exact same width if the design gives them different text gravity.

## 5. Keep live text editable

For homepage work, keep these as live `Text`:

- title
- nav labels
- top action copy
- language labels

Only bake text into art when the typography itself is part of the artwork.

## 6. Use sliced art for the reusable bases

Use `sliced-sprite` for:

- panels
- pills
- button backplates
- toggle backplates

Use `simple-sprite` for:

- logo
- arrows
- small icons

## 7. Treat navigation separately

Do not let route intent drive placement.

First make the page visually right, then mark clickable nodes as:

- `candidate`
- `static`
- or `bound`

Only bind explicit targets.

## 8. Check hierarchy before tweaking fine position

If the page feels messy, inspect in this order:

- missing structural region (shell or region, per your Stage 2 decision)
- wrong parent
- wrong anchor
- wrong pivot
- only then the exact `x/y` offset

This catches most layout problems faster than coordinate tuning.

## 9. Validate the result

Confirm:

- structural region grouping is visible in the hierarchy
- edge-bound nodes are not centered by mistake
- repeated controls read as the same family
- live text is still editable
- sliced assets preserve corners
- screenshots match the design intent
