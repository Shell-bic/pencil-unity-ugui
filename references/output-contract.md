# Output Contract

Unless the user asks for something narrower, answer in this order.

## 1. FitAssessment

One short paragraph stating:

- whether `uGUI` is a good fit
- whether the design looks fixed-screen or adaptive
- whether direct Unity mutation is appropriate for this request

## 2. HierarchyPlan

List the intended tree compactly, for example:

- `Canvas_Main`
- `Screen_Home`
- `Region_Top`
- `Region_LeftNav`
- `Region_Content`
- `Card_Opportunity`
- `Txt_Title`
- `Btn_Opportunity`

## 3. AnchorPlan

For important nodes, state:

- parent
- anchor preset
- fixed or stretch intent

Keep this concise. Focus on nodes whose structural placement matters.

## 4. AssetPlan

State which important visuals should become:

- `simple-sprite`
- `sliced-sprite`
- `text`
- `hit-area`

## 5. ComponentPlan

For important nodes, state the intended Unity component stack, for example:

- `Screen_Home` -> `RectTransform`, optional `CanvasGroup`
- `Panel_Content` -> `RectTransform`, `Image`
- `Btn_Back` -> `RectTransform`, `Image`, `Button`

Focus on nodes whose component choice affects maintainability or behavior.

## 6. TypographyPlan

For important text roles, state:

- tier name
- where the style should come from
- any justified effect components

Keep this compact. Focus on repeated text roles or visually sensitive nodes.

## 7. NavigationPlan

List clickable nodes and their intended targets.

For planning tasks, this is usually enough:

- source
- target
- notes about enlarged hit areas if needed

## 8. PrefabBindingPlan

State:

- what should become a prefab
- what should stay local to the screen
- where route intent and screen behavior should live

## 9. NamingPlan

State the naming convention for:

- hierarchy nodes
- prefabs
- scripts
- route ids
- content keys

## 10. DataBindingPlan

State:

- which content is static
- which content is runtime-driven
- who owns updates
- any localization or media replacement expectations

## 11. ImplementationNotes

State:

- what should be created with `Unity Skills`
- what should be inspected with `Pencil MCP`
- what must remain manual or be verified by screenshot

## 12. ValidationNotes

Check these points explicitly:

- anchor logic
- region grouping
- component selection
- typography consistency
- prefab and binding boundaries
- naming consistency
- data-binding strategy
- sliced sprite usage
- text vs image decisions
- navigation completeness
- screenshot parity assumptions

## Optional sections

Add only when helpful:

- `Risks`
- `ReusePlan`
- `MigrationNotes`
- `WhyNotUIToolkit`
