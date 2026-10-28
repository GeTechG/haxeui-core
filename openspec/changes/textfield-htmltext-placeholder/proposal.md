## Why
On an unfocused `TextField` with a `placeholder`, setting `htmlText` shows the html for a moment and then the placeholder again, with `:empty`. Writing `htmlText` to the text input clears the input's `text`; the input's change callback then copies that empty `text` into the field's `text`, and `TextBehaviour` validates it: no text, so the placeholder goes back over the html. The same path, and every other revalidation (`placeholder`, `maxChars`, `restrictChars`, a focus change), always goes through `text`, so html content is lost whenever one of them runs.

## What Changes
- A text field's content is whichever of `text` and `htmlText` was set last. Only that one is written to the text input; the other one keeps its value but does not drive the display.
- Changing `placeholder`, `maxChars`, `restrictChars` or the focus revalidates the current content: `htmlText` through `validateHtmlText` when it was set last, `text` otherwise.
- While `htmlText` is the content, the input's change callback no longer writes the input's `text` into `text` (that would make `text` the content again); it keeps the stored `htmlText` in step with the input's `htmlText`, and still dispatches `UIEvent.CHANGE`.
- Setting `text` or `htmlText` to the value it already holds makes it the content again when the other one was set after it.

## Capabilities

### New Capabilities

### Modified Capabilities
- `textfield-placeholder`: `:empty` follows the content — `htmlText` when it was set after `text`, `text` otherwise.

## Impact
`haxe/ui/components/TextField.hx` (`TextBehaviour`, `HtmlTextBehaviour`, the behaviours and the focus handler that revalidate, the input's change callback, `TextFieldHelper`). No API change.
