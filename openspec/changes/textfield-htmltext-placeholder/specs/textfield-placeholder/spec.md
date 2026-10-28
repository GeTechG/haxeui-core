## MODIFIED Requirements

### Requirement: `:empty` follows the text, not the displayed string
A `TextField`'s content SHALL be whichever of `text` and `htmlText` was set last (`text` when neither was). The field SHALL show its placeholder and carry `:empty` exactly when it has a placeholder, is not focused, and its content is empty after `maxChars` and `restrictChars` are applied. In every other case it SHALL show its content and SHALL NOT carry `:empty`, whatever that content is — including one equal to the placeholder. While the placeholder is shown the field is not in password mode; otherwise its `password` setting applies. Changing `placeholder`, `maxChars`, `restrictChars` or the focus SHALL keep the content as it is: an `htmlText` content is not replaced by `text`.

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

#### Scenario: Html text kept across revalidation
- **WHEN** an unfocused text field with placeholder `"Name"` has its `htmlText` set to `"Hello"`, then gains and loses focus and has its `placeholder` set to `"Other"`
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
