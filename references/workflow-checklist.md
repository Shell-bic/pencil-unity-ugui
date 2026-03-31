# Workflow Checklist

Use this file for the end-to-end process of translating a Pencil design into Unity uGUI.

## Contents

- Stage 1: Confirm target
- Stage 2: Read the design
- Stage 3: Classify nodes
- Stage 4: Choose layout mode per parent
- Stage 5: Choose anchors
- Stage 6: Choose asset strategy
- Stage 7: Choose component stack
- Stage 8: Choose typography and visual rules
- Stage 9: Choose prefab and binding boundaries
- Stage 10: Choose naming conventions
- Stage 11: Choose content and data-binding rules
- Stage 12: Create or describe hierarchy
- Stage 13: Use Unity Skills
- Stage 14: Add navigation
- Stage 15: Verify
- Minimum output for planning

## Stage 1: Confirm target

Confirm:

- target technology is `uGUI`
- source of truth is `Pencil MCP`, screenshot, or structured layout spec
- user wants either planning, implementation, or review

If the user only wants architecture or feasibility, stop at planning and do not mutate Unity.

## Stage 2: Read the design

Use `Pencil MCP` to inspect:

- top-level frames across the whole file when the document may contain multiple related pages
- top-level screen bounds
- major regions
- repeated structures
- screenshot for visual verification
- loose assets, reference boards, or scratch areas that should not be treated as pages

If the file contains multiple pages from one system, first identify:

- shared shell regions
- page families
- reusable controls
- pages that are only variations of the same template

If the user's top priority is likeness rather than framework completeness, select the currently focused page as the visual baseline page and verify that one first.

Identify the page type:

- fixed-screen dashboard
- panel-based page
- list/grid page
- popup/dialog
- overlay/HUD

## Stage 3: Classify nodes

Classify meaningful nodes into:

- `screen-root`
- `region`
- `container`
- `panel`
- `image`
- `text`
- `decoration`
- `hit-area`
- `nav-control`

This classification is mandatory before Unity creation.

When working with multi-page large-screen systems, also classify:

- `shared-shell`
- `page-template`
- `page-specific-content`
- `reference-asset`

## Stage 4: Choose layout mode per parent

Choose one layout mode per parent:

- `fixed-placement`
- `layout-group`

Use `fixed-placement` when:

- elements are part of a static composition
- a large-screen layout depends on precise placement
- the design is image-heavy

Use `layout-group` when:

- children repeat in a row, column, or grid
- spacing is regular
- adaptation is structural, not artistic

Do not mix both approaches under the same parent unless a wrapper container isolates the behavior.

Before finalizing layout mode, ask:

- is the parent a shell region, a content panel, or a true repeated flow?
- does the design want a visually fixed composition or a structurally repeating arrangement?
- would a wrapper region make the hierarchy easier to understand later?

## Stage 5: Choose anchors

Use [anchor-rules.md](anchor-rules.md).

Decide anchors before creating Unity nodes.

For Pencil-to-Unity translation, treat the page as a top-left design canvas first, then map each node into Unity's anchor/pivot space.

For each important node, record:

- parent
- anchor preset
- pivot intent if important
- fixed size or stretch intent

If a node belongs to an edge or region, anchor it to that region first instead of compensating from the Canvas root with a large offset.

## Stage 6: Choose asset strategy

Use [asset-rules.md](asset-rules.md).

For each visual node, record:

- `simple-sprite`
- `sliced-sprite`
- `text`
- `hit-area`

For high-fidelity fixed-screen work, default key controls to `background cutout art + live text + transparent hit layer` before falling back to pure color approximation.

If a reusable rounded panel is marked `simple-sprite`, re-check that decision.

## Stage 7: Choose component stack

Use [component-rules.md](component-rules.md).

For each important node, record the intended Unity component stack.

At minimum, resolve:

- whether the node is `Image` or `RawImage`
- whether text should stay `Text`
- whether interaction belongs on the visual node or a separate hit area
- whether `CanvasGroup` is needed for page or region state
- whether layout, masking, or scrolling components are actually justified

## Stage 8: Choose typography and visual rules

Use [typography-visual-rules.md](typography-visual-rules.md).

For important text and styled nodes, record:

- typography tier
- whether styling should come from text settings, sprite art, or effect components
- whether any effect components are justified

## Stage 9: Choose prefab and binding boundaries

Use [prefab-binding-rules.md](prefab-binding-rules.md).

For each important cluster, decide:

- should it stay local or become a prefab
- does behavior belong to a screen controller or an element-level script
- where route intent should live

For multi-page systems, prefer this order:

- shared shell prefab candidates first
- repeated controls second
- page-local content last

## Stage 10: Choose naming conventions

Use [naming-rules.md](naming-rules.md).

For important nodes and systems, decide:

- hierarchy prefixes
- prefab names
- script names
- route ids
- content keys

## Stage 11: Choose content and data-binding rules

Use [data-binding-rules.md](data-binding-rules.md).

For important content nodes, decide:

- static assignment or runtime assignment
- who owns updates
- whether localization or media replacement is expected
- how text, image, and route content should be keyed

## Stage 12: Create or describe hierarchy

Preferred naming:

- `Canvas_*`
- `Screen_*`
- `Region_*`
- `Panel_*`
- `Card_*`
- `Img_*`
- `Txt_*`
- `Btn_*`
- `Hit_*`

The hierarchy should group by region first, not by asset type alone.

When the design feels visually cluttered, regroup the tree by shell regions first:

- `Shell_*`
- `Region_*`
- `Panel_*`
- local content

Then check whether edge-bound controls were mistakenly treated as centered elements.

## Stage 13: Use Unity Skills

Only when direct implementation is requested:

- load and follow the `unity-skills` and `unity-ui` skill rules
- ensure the user has explicitly requested direct Unity mutation
- treat UI creation as `full-auto` work
- create the Canvas or reuse the existing one
- keep default scene infrastructure such as `Main Camera`, `Directional Light`, and `Global Volume` unless there is a concrete reason to remove it
- create major regions first
- create repeated UI in batches when possible
- set anchors before final rect tuning
- use layout skills only where justified
- after script writes or asset imports, re-check editor automation health before treating a menu-execution failure as an implementation failure

If Unity mutation is not requested, describe these actions instead of executing them.

## Stage 14: Add navigation

Build navigation only after the visual hierarchy is stable.

For each clickable node, record:

- source node
- route intent
- target screen/panel/state
- whether the click area should be larger than the art

Keep route intent separate from styling.

If the design shows a clickable-looking control but not its explicit target:

- mark it as `candidate`
- keep it static or unbound in implementation
- do not invent cross-page mappings from visual similarity alone

## Stage 15: Verify

Verification should check:

- hierarchy matches the intended regions
- anchors express structural intent
- the design-to-Unity coordinate translation is consistent with the chosen parent and anchor
- component stacks match node roles
- typography roles are consistent
- prefab and binding boundaries are intentional
- naming is consistent and role-driven
- binding complexity matches the actual screen needs
- sliced sprites are used where resizing must preserve corners
- click targets are usable
- repeated structures are actually reused
- navigation paths are complete
- the result still matches the design screenshot
- key hero controls such as primary pills and language toggles are not over-generalized into visibly wrong proportions
- major content is not hidden behind another sibling because of Canvas child order

## Minimum output for planning

At a minimum, output:

- fit assessment
- page-family or shell assessment when relevant
- hierarchy plan
- anchor plan
- asset plan
- navigation plan
- risk list

Use [output-contract.md](output-contract.md) unless the user asks for a different format.
