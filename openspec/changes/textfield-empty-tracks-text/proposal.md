## Why
`TextFieldHelper.validateText` (and `validateHtmlText`) decides whether a `TextField` shows its placeholder (the `:empty` class) by comparing the string it is given with `placeholder`. Without focus, a non-empty text equal to the placeholder leaves `:empty` in place, so real text is drawn in the placeholder's style until focus changes. With no placeholder, `:empty` is removed only for an empty text, so clearing `placeholder` while a non-empty text is shown keeps `:empty` too. The string the helpers receive is always the behaviour value (`text` / `htmlText`), never the displayed placeholder, so comparing it with the placeholder tells nothing.

## What Changes
- Without focus and with a placeholder, a non-empty text removes `:empty` and restores the password mode, whatever its value.
- With no placeholder, `:empty` is removed whatever the text.
- The same for `htmlText`.

## Capabilities

### New Capabilities
- `textfield-placeholder`: when a text field shows its placeholder and carries `:empty`.

### Modified Capabilities

## Impact
`haxe/ui/components/TextField.hx` (`TextFieldHelper`). No API change.
