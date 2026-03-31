# uGUI Screen Plan Template

## FitAssessment

- screen type:
- is uGUI a good fit:
- planning only or implementation:

## ScreenSummary

- screen name:
- design source:
- primary interaction model:

## HierarchyPlan

- `Canvas_Main`
- `Screen_<Name>`
- `Region_Top`
- `Region_Left`
- `Region_Content`

## AnchorPlan

| Node | Parent | Anchor | Fixed/Stretch | Notes |
|------|--------|--------|---------------|-------|
| `Screen_<Name>` | `Canvas_Main` | `StretchAll` | Stretch | |

## AssetPlan

| Node | Type | Unity Target | Reusable | Notes |
|------|------|--------------|----------|-------|
| `Bg_Full` | `simple-sprite` | `Image` | No | |

## ComponentPlan

| Node | Components | Notes |
|------|------------|-------|
| `Screen_<Name>` | `RectTransform`, `CanvasGroup` (optional) | |
| `Panel_Content` | `RectTransform`, `Image` | |
| `Btn_Back` | `RectTransform`, `Image`, `Button` | |

## TypographyPlan

| Role | Tier | Source | Effects | Notes |
|------|------|--------|---------|-------|
| `Txt_Title` | `Title` | `Text` settings | none | |

## NavigationPlan

| Source | Target | Click Layer | Notes |
|--------|--------|-------------|-------|
| `Btn_Back` | `Screen_Home` | `Btn_Back` | |

## PrefabBindingPlan

| Cluster | Prefab? | Script Owner | Route Owner | Notes |
|---------|---------|--------------|-------------|-------|
| `Panel_Content` | No | `UIScreenController` | n/a | |
| `Btn_Back` | No | `UIScreenController` | `UIRouter` | |

## NamingPlan

| Kind | Convention | Example |
|------|------------|---------|
| Hierarchy | `Screen_`, `Region_`, `Panel_`, `Btn_`, `Txt_` | `Screen_Home` |
| Prefab | role-driven | `Card_Primary` |
| Script | responsibility-driven | `HomeScreenController` |
| Route | short stable id | `Home` |
| Content Key | semantic snake_case | `title` |

## DataBindingPlan

| Field/Cluster | Static or Runtime | Owner | Notes |
|---------------|-------------------|-------|-------|
| `Txt_Title` | Static | scene/prefab | |
| `Img_Hero` | Runtime | `UIScreenController` | |

## Risks

- 

## ValidationChecklist

- anchors match structural intent
- sliced sprites are used where corners must be preserved
- component stacks match node roles
- typography roles are consistent
- prefab and binding boundaries are intentional
- naming is consistent and role-driven
- binding complexity matches screen needs
- click targets are usable
- hierarchy is grouped by region
