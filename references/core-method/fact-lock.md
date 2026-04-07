# Page Truth And Shared Component Fact Lock

Use this reference whenever the task involves page-state mapping or shared shell components.

## When Fact Lock Is Mandatory

Run a fact lock before implementation when any of the following is true:
- The user compares multiple Pencil pages and asks how navigation, shell regions, or page states relate
- A shared shell region appears across pages, such as left navigation, top command buttons, language toggles, playback bars, or persistent side rails
- The user disputes sizing, spacing, visibility, or interaction based on the current design
- There is any risk of confusing local content buttons with global navigation

## Required Outputs

Produce both artifacts below before implementation:

### 1. `PageTruthMap`

For each referenced page, record:
- `PageId` or page name
- Active primary navigation item
- Whether secondary navigation is shown
- Which secondary item is selected, if any
- Which shell regions are visible or hidden
- Which right-side content state is displayed

### 2. `SharedComponentFactTable`

For each shared component family, record:
- Component family name
- Source page(s)
- Exact geometry from the current `.pen`
- Notable visibility or state rules
- Any structural notes that affect Unity implementation

Recommended component families:
- Left primary navigation
- Left secondary navigation
- Top command buttons
- Language toggles
- Playback bar
- Persistent auxiliary rails

## Source Of Truth Rule

If the current `.pen` is available:
- Use the current `.pen` as the source of truth
- Use screenshots only as comparison support
- Do not size or map shared components from historical Unity output

## Hard Anti-Patterns

Treat the following as invalid:
- Inferring left-side child navigation from right-side content chips
- Treating a landing page as expanded just because another page in the same theme is expanded
- Reusing old screenshot measurements when current Pencil geometry is available
- Assuming two visually similar pages share the same page-state mapping without checking both pages
