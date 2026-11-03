## MODIFIED Requirements

### Requirement: `:empty` follows the text, not the displayed string
A `TextField`'s content SHALL be whichever of `text` and `htmlText` was set last (`text` when neither was). The field SHALL show its placeholder and carry `:empty` exactly when it has a placeholder, is not focused, and its content is empty after `maxChars` and `restrictChars` are applied; otherwise it SHALL show its content without `:empty`, even a content equal to the placeholder.

#### Scenario: Text equal to the placeholder
- **WHEN** an unfocused text field with placeholder `"Name"` and an empty text has its `text` set to `"Name"`
- **THEN** it does not have `:empty`

#### Scenario: Placeholder removed under a non-empty text
- **WHEN** an unfocused text field with a placeholder and an empty text has its `text` set to `"Name"` and then its `placeholder` set to `null`
- **THEN** it does not have `:empty`

#### Scenario: Text cleared
- **WHEN** an unfocused text field with placeholder `"Name"` has its `text` set to `""`
- **THEN** it has `:empty` and shows `"Name"`

#### Scenario: Html text set
- **WHEN** an unfocused text field with placeholder `"Name"` and an empty text has its `htmlText` set to `"Hello"`
- **THEN** it does not have `:empty` and its text input's `htmlText` is `"Hello"`

#### Scenario: Html text cleared
- **WHEN** an unfocused text field with placeholder `"Name"` has its `htmlText` set to `"Hello"` and then to `""`
- **THEN** it has `:empty` and shows `"Name"`

#### Scenario: Text set after html text
- **WHEN** an unfocused text field with placeholder `"Name"` has its `htmlText` set to `"Hello"` and then its `text` set to `"Hi"`
- **THEN** it does not have `:empty` and its text input's `text` is `"Hi"`

#### Scenario: Clone
- **WHEN** a text field with placeholder `"Name"` has its `htmlText` set to `"X"`, then its `text` set to `"Hi"`, and is cloned
- **THEN** the clone shows `"Hi"` as text, not `"X"` as html

#### Scenario: Html text kept across revalidation
- **WHEN** an unfocused text field with placeholder `"Name"` has its `htmlText` set to `"Hello"`, then gains and loses focus and has its `placeholder` set to `"Other"`
- **THEN** it does not have `:empty` and its text input's `htmlText` is `"Hello"`

#### Scenario: Content reduced to nothing
- **WHEN** an unfocused text field with placeholder `"123"` and `restrictChars` `"0-9"` has its `htmlText` set to `"abc"` and then its `placeholder` set to `"456"`
- **THEN** it has `:empty`, shows `"456"`, and its `htmlText` is `""`

## ADDED Requirements

### Requirement: The placeholder is never masked
While a `TextField` shows its placeholder it SHALL NOT be in password mode; while it shows its content its `password` setting SHALL apply.

#### Scenario: Password field with a placeholder
- **WHEN** an unfocused text field with placeholder `"Password"`, `password = true` and an empty text has its `text` set to `"secret"`
- **THEN** before the change its text input shows `"Password"` unmasked, and after it the text input is in password mode

### Requirement: Revalidation keeps the content
Changing a `TextField`'s `placeholder`, `maxChars`, `restrictChars` or focus SHALL keep its content as it is: an `htmlText` content is not replaced by `text`.

#### Scenario: Html text kept when maxChars changes
- **WHEN** an unfocused text field with placeholder `"Name"` has its `htmlText` set to `"Hello"` and then its `maxChars` set to `10`
- **THEN** it does not have `:empty` and its text input's `htmlText` is `"Hello"`

