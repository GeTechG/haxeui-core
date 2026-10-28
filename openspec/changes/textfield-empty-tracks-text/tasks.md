## 1. Implement
- [ ] 1.1 `TextFieldHelper.validateText`: without focus, a non-empty text removes `:empty` without comparing it with the placeholder; with no placeholder, `:empty` is removed for any text
- [ ] 1.2 `TextFieldHelper.validateHtmlText`: the same

## 2. Verify
- [ ] 2.1 Typing check exits 0
- [ ] 2.2 Script under `--interp` against the display backend: the scenarios of `textfield-placeholder` for `text` and `htmlText`
