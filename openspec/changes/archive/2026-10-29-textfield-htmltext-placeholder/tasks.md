## 1. Implement
- [x] 1.1 Track whether `htmlText` or `text` was set last; setting either one, even to its current value, makes it the content
- [x] 1.2 `TextBehaviour` / `HtmlTextBehaviour` validate only while they hold the content
- [x] 1.3 `TextFieldHelper.validate`: revalidate the current content; use it for `placeholder`, `maxChars`, `restrictChars` and focus changes
- [x] 1.4 The input's change callback: while `htmlText` is the content, write the input's `htmlText` into `htmlText` instead of its `text` into `text`
- [x] 1.5 `validateText` / `validateHtmlText` clear the other kind of content in the text input
- [x] 1.6 `TextBehaviour` / `HtmlTextBehaviour` store `""`, not the placeholder, when the placeholder is shown
- [x] 1.7 `postCloneComponent` gives the clone the source's content

## 2. Verify
- [x] 2.1 Typing check exits 0
- [x] 2.2 Script under `--interp` against the display backend: the scenarios of `textfield-placeholder`
