# eval-runtime Specification

## Purpose
Say that the library runs on the eval target (`--interp`) against the display backend, so behaviour can be checked without a real backend.

## Requirements

### Requirement: The library runs under --interp
A program built with `--interp` against the library and the display backend in `tools/display-backend` SHALL start, run `Toolkit.init()` (including parsing the default theme) and create and drive components — among them an `InteractiveComponent` such as `Button`, through `disabled`, `value` and `disableInteractivity` — without a runtime error, and with the same results as the same program built for js and run under node.

#### Scenario: Startup
- **WHEN** a program that creates a `Button` is run with `--interp` against the display backend
- **THEN** it reaches `main` instead of failing on a missing field of an interface it implements

#### Scenario: Toolkit initialisation
- **WHEN** that program calls `Toolkit.init()`
- **THEN** the default theme is parsed without an exception

#### Scenario: Same results as js
- **WHEN** the program sets `disabled`, `value` and calls `disableInteractivity` on the button and prints them
- **THEN** it prints the same under `--interp` as its js build under node
