# button-pointer-states Specification

## Purpose
Say when a button takes the `:hover` and `:down` pointer states.

## Requirements

### Requirement: A button with interactivity disabled takes no pointer states
While a button's interactivity is disabled (`disableInteractivity(true, …)`, including through `disabled = true`), `ButtonEvents` SHALL NOT add `:hover` or `:down` to it in response to the pointer — neither when the button moves or relayouts under the pointer (`UIEvent.MOVE`) nor when a press that began before the disable is released over it. Such a release SHALL still end the press: `:down` is removed and the repeat timer stops. Once interactivity is enabled again, both paths SHALL add `:hover` when the pointer is over the button, as before.

#### Scenario: Relayout under a still pointer
- **WHEN** a button whose interactivity is disabled moves under the pointer and receives `UIEvent.MOVE`
- **THEN** it does not have `:hover`

#### Scenario: Disabled between press and release
- **WHEN** a button is pressed, its interactivity is disabled, and the pointer is released over it
- **THEN** it has neither `:down` nor `:hover`

#### Scenario: Interactivity enabled again
- **WHEN** interactivity of that button is enabled again and it moves under the pointer
- **THEN** it has `:hover`
