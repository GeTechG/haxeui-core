## Why
On an unfocused `TextField` with a `placeholder`, setting `htmlText` shows the html for a moment and then the placeholder again, with `:empty`. Writing `htmlText` to the text input clears the input's `text`; the input's change callback then copies that empty `text` into the field's `text`, and `TextBehaviour` validates it: no text, so the placeholder goes back over the html. The same path, and every other revalidation (`placeholder`, `maxChars`, `restrictChars`, a focus change), always goes through `text`, so html content is lost whenever one of them runs.

## What Changes
- A text field's content is whichever of `text` and `htmlText` was set last. Only that one is written to the text input; the other one keeps its value but does not drive the display.
- Changing `placeholder`, `maxChars`, `restrictChars` or the focus revalidates the current content: `htmlText` through `validateHtmlText` when it was set last, `text` otherwise.
- While `htmlText` is the content, the input's change callback writes the input's `htmlText` into `htmlText` instead of its `text` into `text` (that would make `text` the content again), so an edit is validated — `maxChars`, `restrictChars`, the placeholder — the same way as in a plain text field. It still dispatches `UIEvent.CHANGE`.
- Writing one kind of content to the text input clears the other one there: `validateText` clears the input's `htmlText`, `validateHtmlText` its `text` — also when the html is the same as before, which `TextInput.set_htmlText` would otherwise ignore.
- A clone takes the same content as its source: the clone macro copies `text` and then a non-null `htmlText`, which picks the wrong one when `text` was set after `htmlText`, or `htmlText` set to `null` after `text`; `TextField.postCloneComponent` sets the source's content once more.
- Setting `text` or `htmlText` to the value it already holds makes it the content again when the other one was set after it.

## Capabilities

### New Capabilities

### Modified Capabilities
- `textfield-placeholder`: `:empty` follows the content — `htmlText` when it was set after `text`, `text` otherwise.

## Impact
`haxe/ui/components/TextField.hx` (`TextBehaviour`, `HtmlTextBehaviour`, the behaviours and the focus handler that revalidate, the input's change callback, `TextFieldHelper`, `postCloneComponent`). No API change.
