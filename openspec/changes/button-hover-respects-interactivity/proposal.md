## Why
`disableInteractivity(true, …)` unregisters a button's interactive events (mouse over/out/down, click), but `ButtonEvents` still sets `:hover` from two paths it does not touch: the `UIEvent.MOVE` listener (`onMove`), which is not an interactive event and stays registered, and the screen-level `MOUSE_UP` listener (`onMouseUp`) that `onMouseDown` registers, which still fires when interactivity is disabled between press and release. A button that ignores the pointer then shows the hover look whenever it moves or relayouts under a still pointer, or is released over.

## What Changes
- `ButtonEvents.onMove` does not add `:hover` while the button's interactivity is disabled (it still removes it when the pointer is outside).
- `ButtonEvents.onMouseUp` still ends the press (clears the pressed state, the repeat timer, `:down`, unregisters itself) but does not add `:hover` while the button's interactivity is disabled.
- With interactivity enabled again, both behave as before.

## Capabilities

### New Capabilities
- `button-pointer-states`: when a button takes the `:hover` and `:down` pointer states, and that it does not while its interactivity is disabled.

### Modified Capabilities

## Impact
`haxe/ui/components/Button.hx` (`ButtonEvents`). No API change.
