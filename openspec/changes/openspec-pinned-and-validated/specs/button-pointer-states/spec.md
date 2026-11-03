## MODIFIED Requirements

### Requirement: A button with interactivity disabled takes no pointer states
While a button's interactivity is disabled (`disableInteractivity(true, …)`, including through `disabled = true`), `ButtonEvents` SHALL NOT add `:hover` or `:down` to it in response to the pointer: neither when it moves or relayouts under the pointer (`UIEvent.MOVE`) nor when a press that began before the disable is released over it.

#### Scenario: Relayout under a still pointer
- **WHEN** a button whose interactivity is disabled moves under the pointer and receives `UIEvent.MOVE`
- **THEN** it does not have `:hover`

#### Scenario: Disabled between press and release
- **WHEN** a button is pressed, its interactivity is disabled, and the pointer is released over it
- **THEN** it has neither `:down` nor `:hover`

#### Scenario: Interactivity enabled again
- **WHEN** interactivity of that button is enabled again and it moves under the pointer
- **THEN** it has `:hover`

## ADDED Requirements

### Requirement: A release still ends the press of a disabled button
When a press that began before the button's interactivity was disabled is released over it, `ButtonEvents` SHALL end the press: it removes `:down` and stops the repeat timer.

#### Scenario: Repeating button disabled while held
- **WHEN** a button with `repeater = true` is pressed, its interactivity is disabled, and the pointer is released over it
- **THEN** it does not have `:down` and the repeat timer no longer dispatches clicks

### Requirement: Pointer states return with interactivity
Once a button's interactivity is enabled again, `ButtonEvents` SHALL add `:hover` to it when the pointer is over it, both on `UIEvent.MOVE` and on a release, as before the disable.

#### Scenario: Release after interactivity is enabled again
- **WHEN** a button whose interactivity was disabled and enabled again is pressed and the pointer is released over it
- **THEN** it has `:hover` and not `:down`
