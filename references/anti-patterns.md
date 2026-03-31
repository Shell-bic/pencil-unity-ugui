# Anti-patterns

Read this file when the task is ambiguous or when prior attempts mixed incompatible UI models.

## Common confusions

- `RectTransform` is not browser `Flexbox`
- `uGUI` is not `UI Toolkit`
- a design grouping is not automatically a `LayoutGroup`
- a beautiful flat export is not automatically a good interactive UI asset

## Bad patterns

### 1. Center-anchor everything

Symptom:

- every node uses `MiddleCenter`
- large positive/negative coordinates compensate for bad anchoring

Why it is bad:

- brittle hierarchy
- poor maintainability
- confusing future edits

### 2. Make everything a layout group

Symptom:

- fixed exhibition screens are rebuilt as nested horizontal/vertical groups everywhere

Why it is bad:

- fights the original composition
- creates confusing rect behavior
- increases manual overrides

### 3. Flatten the hierarchy

Symptom:

- dozens of nodes directly under `Canvas`

Why it is bad:

- no structural grouping
- anchors become harder to reason about
- navigation and reuse suffer

### 4. Stretch rounded assets as simple sprites

Symptom:

- pills and cards deform when resized

Why it is bad:

- visible corner warping
- inconsistent border thickness

### 5. Bake all text into images

Symptom:

- labels, titles, and data all become PNGs

Why it is bad:

- poor maintainability
- no localization path
- worse clarity at runtime

### 6. Attach clicks directly to decorative art without hit-area review

Symptom:

- click area equals the visible pixels of a small or irregular sprite

Why it is bad:

- poor touch usability
- fragile interaction targets

## Recovery guidance

When one of these patterns appears:

- stop creating more nodes
- re-classify the design
- rebuild the parent strategy first
- then reapply anchors, assets, and navigation
