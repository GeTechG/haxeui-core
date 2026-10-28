## ADDED Requirements

### Requirement: `:empty` follows the text, not the displayed string
A `TextField` SHALL show its placeholder and carry `:empty` exactly when it has a placeholder, is not focused, and its `text` is empty after `maxChars` and `restrictChars` are applied. In every other case it SHALL show its text and SHALL NOT carry `:empty`, whatever that text is — including a text equal to the placeholder. While the placeholder is shown the field is not in password mode; otherwise its `password` setting applies.

#### Scenario: Text equal to the placeholder
- **WHEN** an unfocused text field with placeholder `"Name"` and an empty text has its `text` set to `"Name"`
- **THEN** it does not have `:empty`

#### Scenario: Placeholder removed under a non-empty text
- **WHEN** an unfocused text field with a placeholder and an empty text has its `text` set to `"Name"` and then its `placeholder` set to `null`
- **THEN** it does not have `:empty`

#### Scenario: Text cleared
- **WHEN** an unfocused text field with placeholder `"Name"` has its `text` set to `""`
- **THEN** it has `:empty` and shows `"Name"`
