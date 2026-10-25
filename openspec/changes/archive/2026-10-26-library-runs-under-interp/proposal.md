## Why
A program built against the do-nothing backend (`tools/display-backend`) with `--interp` dies before `main` runs: `Field index for get_disabled not found on prototype haxe.ui.core.InteractiveComponent`. The eval target fails to build the interface table of a class whose interface property accessors are all inherited from a superclass (reproducible without HaxeUI, in the Haxe 5 fork and in Haxe 4.3.6): `InteractiveComponent` implements `IFocusable` (`disabled`) and `IValueComponent` (`value`), whose accessors are generated on `ComponentBase`. Past that, `Toolkit.init()` throws `Null Access` while parsing the default theme: two `EReg.map` callbacks in the CSS parser return `null` for a `String`, which eval rejects (js inserts `"null"` into a result that is discarded). Behaviour checks of the library therefore need a js build and node with stubs instead of a plain `--interp` run.

## What Changes
- `InteractiveComponent` redeclares `get_disabled`/`set_disabled` and `get_value`/`set_value` as overrides that only call `super`, so eval finds them on the class that implements the interfaces. No behaviour change on any target.
- The two `EReg.map` callbacks in `haxe.ui.styles.Parser` whose result is discarded return `""` instead of `null`. No behaviour change on any target.

## Capabilities

### New Capabilities
- `eval-runtime`: the library initialises and runs component code on the eval target (`--interp`) against the display backend, so behaviour checks need no real backend.

### Modified Capabilities

## Impact
`haxe/ui/core/InteractiveComponent.hx`, `haxe/ui/styles/Parser.hx`. No API change. The underlying eval bug is filed against the compiler fork separately.
