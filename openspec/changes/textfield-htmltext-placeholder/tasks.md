## 1. Implement
- [ ] 1.1 Track whether `htmlText` or `text` was set last; setting either one, even to its current value, makes it the content
- [ ] 1.2 `TextBehaviour` / `HtmlTextBehaviour` validate only while they hold the content
- [ ] 1.3 `TextFieldHelper.validate`: revalidate the current content; use it for `placeholder`, `maxChars`, `restrictChars` and focus changes
- [ ] 1.4 The input's change callback: while `htmlText` is the content, keep `htmlText` in step with the input instead of writing `text`

## 2. Verify
- [ ] 2.1 Typing check exits 0
- [ ] 2.2 Script under `--interp` against the display backend: the scenarios of `textfield-placeholder`
