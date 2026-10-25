## 1. Implement
- [ ] 1.1 `InteractiveComponent`: override the `disabled` and `value` accessors with calls to `super`
- [ ] 1.2 `Parser`: the discarded `EReg.map` callbacks return `""`, not `null`
- [ ] 1.3 File the eval bug (inherited interface accessors) against the compiler fork, with a HaxeUI-free reproduction

## 2. Verify
- [ ] 2.1 Typing check exits 0
- [ ] 2.2 Under `--interp` against the display backend: `Toolkit.init()`, a `Button`, `disableInteractivity(true)`, `disabled = true`, `value = …` run to the end, and print the same as the js build of the same program run under node
