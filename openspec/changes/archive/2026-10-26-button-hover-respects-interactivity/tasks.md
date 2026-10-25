## 1. Implement
- [x] 1.1 `ButtonEvents.onMove`: no `:hover` while interactivity is disabled
- [x] 1.2 `ButtonEvents.onMouseUp`: end the press, but no `:hover` while interactivity is disabled

## 2. Verify
- [x] 2.1 Typing check exits 0
- [x] 2.2 Script against the display backend (js, run under node; `--interp` does not run the library): a button with interactivity disabled under the pointer relayouts and stays without `:hover`; a button disabled between press and release over it stays without `:hover`; after `disableInteractivity(false)` both paths set `:hover` again
