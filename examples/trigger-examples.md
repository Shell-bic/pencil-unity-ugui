# Trigger Examples

Use this file when deciding whether `pencil-unity-ugui` is the right skill for the request.

## Should trigger

- "Use Pencil MCP to turn this kiosk design into a Unity uGUI hierarchy."
- "Based on this .pen layout, plan the anchors and sliced sprites for a control-room screen."
- "Translate this exhibition dashboard design into uGUI and tell me which parts should be fixed-placement."
- "I have a Pencil layout and want a Unity Canvas plan, route map, and asset slicing plan."
- "Review whether this Pencil-to-uGUI conversion should use layout groups or fixed placement."

## Should usually not trigger

- "Add a button to my existing Unity Canvas."
- "Fix the color of this uGUI panel."
- "Write a generic Unity UI menu with no design source."
- "Move this existing RectTransform 20 pixels to the right."
- "Refactor this UI Toolkit screen."

These should usually use the general Unity UI or Unity Skills paths instead.

## Borderline cases

- Screenshot only, no Pencil file:
  - Trigger if the task is still clearly design-to-uGUI translation.
- Existing uGUI screen review:
  - Trigger only if the review is design-translation-oriented, not a pure implementation bugfix.
- Mixed comparison:
  - Trigger if the user is explicitly comparing Pencil-driven uGUI against another UI system.

## Quick decision rule

Trigger this skill when both are true:

1. The target is `Unity uGUI`
2. The task depends on reading or reconstructing design structure, not just editing existing Unity UI
