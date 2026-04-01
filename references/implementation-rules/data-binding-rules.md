# Data Binding Rules

Use this file when deciding how text, images, and navigation-related content should be assigned or updated in a Pencil-to-uGUI workflow.

## Contents

- Principle
- Default binding stance
- Static content assignment
- Runtime data binding
- Localization and text replacement
- Image and media replacement
- Controller responsibilities
- Anti-patterns
- Agent checklist

## Principle

Do not introduce runtime binding complexity unless the screen actually needs it.

A Pencil-derived exhibition screen is often mostly static. The binding approach should stay as simple as the product need allows.

## Default binding stance

Default to:

- static assignment in scene or prefab
- explicit runtime updates from a screen controller when needed

Do not assume a generic binding framework unless the project already has one.

## Static content assignment

Prefer static assignment when:

- text is fixed
- art is fixed
- the design is a showcase screen
- content only changes between builds, not during runtime

Good fits:

- titles
- menu labels
- decorative badges
- static background images

## Runtime data binding

Use explicit runtime binding when:

- content depends on scene state
- values come from configuration or backend data
- language or mode changes at runtime
- a screen controller must update multiple sibling fields together

Prefer:

- one-way explicit assignment
- clear field references
- grouped update methods at screen scope

## Localization and text replacement

When text may change by language:

- keep text nodes live, not baked into art
- use stable content keys
- centralize language-sensitive assignment where possible

Do not scatter language replacement logic across unrelated button objects.

## Image and media replacement

Use explicit replacement when:

- a panel art changes by state
- a gallery or media tile is data-driven
- a logo or badge can change by content pack

Prefer:

- clear sprite reference fields
- one controller deciding the current visual state

## Controller responsibilities

Prefer this split:

- local visual nodes render assigned content
- screen controller assigns grouped content
- router handles navigation transitions
- reusable prefab scripts only manage local visual state when needed

## Anti-patterns

- Do not introduce a complex binding layer for a mostly static screen.
- Do not hardcode repeated text assignment separately on many child nodes if one screen controller owns the state.
- Do not bury route target data in random visual fields.
- Do not mix static scene assignment and hidden runtime overwrite without documenting the precedence.

## Agent checklist

Before finalizing binding strategy, ask:

- Is this content actually dynamic?
- Could static assignment be enough?
- Which object should own updates: screen controller, router, or reusable prefab?
- Are text, image, and route values named in a way that can survive later growth?
