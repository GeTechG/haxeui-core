# toolchain Specification

## Purpose
Say which compiler builds the library and give every checkout that compiler and symbol navigation with one command.

## Requirements

### Requirement: The compiler is pinned in the repository
`tools/haxe-build.pin` SHALL hold one line, `<build key, 40 hex> <sha256 of the archive, 64 hex>`, naming the file `haxe-linux64-<key>.tar.gz` of the `builds` release of `GeTechG/haxe`. The library SHALL be built, typed and tested only with that compiler (`.haxe/haxe`, `HAXE_STD_PATH=.haxe/std`); changing the compiler is a change of that file alone.

#### Scenario: Compiler bump
- **WHEN** the pin file is changed to another key and checksum and `tools/setup.sh` is run
- **THEN** `.haxe` points at the install of the new key and the install of the old key is left in place

### Requirement: One command sets up a checkout
`tools/setup.sh` SHALL download the pinned build, verify its checksum, install it in a per-key directory of the user's cache shared by all checkouts, and point the gitignored `.haxe` symlink at it. It SHALL refuse an archive whose checksum differs from the pin, SHALL NOT download again when the key is already installed, SHALL refuse an install that was verified against another checksum than the pin's, and SHALL refuse to link when `.haxe` is a real directory.

#### Scenario: Fresh worktree
- **WHEN** `tools/setup.sh` is run in a new worktree
- **THEN** `.haxe/haxe --version` reports the pinned build

#### Scenario: Checksum mismatch
- **WHEN** the downloaded archive does not match the checksum in the pin file
- **THEN** the command fails, names both checksums, and installs nothing

### Requirement: Serena navigates the sources with the pinned compiler
The setup command SHALL build `vshaxe/haxe-language-server` from source at a fixed commit into a per-commit directory of the user's cache, and write the gitignored `.serena/project.local.yml` so that Serena starts that server with `.haxe` first on its `PATH`. It SHALL create a minimal `.serena/project.yml` when none exists, and SHALL NOT overwrite a `project.local.yml` it did not generate. Serena SHALL be registered in `.mcp.json` and `.codex/config.toml`.

#### Scenario: Reference lookup
- **WHEN** Serena's `find_referencing_symbols` is asked for a symbol of the library after the setup command
- **THEN** it returns the references and the server log shows `Using --server-connect`

#### Scenario: Someone's own overrides
- **WHEN** `.serena/project.local.yml` exists with settings and without the generator's mark
- **THEN** the command fails and leaves the file as it is

### Requirement: The display config types every module
The generated display config SHALL hold only class paths, defines and module names (no `-lib`, no `--macro`), SHALL supply a backend so the library types on its own, and SHALL name every module of its class paths except `import.hx`, the macro package and the modules the setup command lists as not typing on their own. `.haxe/haxe <display config> --no-output` SHALL exit 0; the setup command warns when it does not.

#### Scenario: New source file
- **WHEN** a module is added and the setup command is run again
- **THEN** the display config names the new module

### Requirement: Reference lists are checked against a text search
`AGENTS.md` SHALL state that language-server reference lists are not exhaustive and that a rename or removal is preceded by a text search.

#### Scenario: Conditional code
- **WHEN** a call site sits behind a compile-time conditional the display config does not define
- **THEN** the language server does not report it and the text search does

### Requirement: Structural search works on the Haxe sources
The setup command SHALL download the `ast-grep` binary at a fixed version, refuse an archive whose sha256 differs from the one it pins, and build the Haxe grammar `GeTechG/tree-sitter-haxe` at a fixed commit, each into a per-pin directory of the user's cache shared by all checkouts, and link them as `.ast-grep/ast-grep` and `.ast-grep/haxe.so` in the gitignored `.ast-grep/` directory. `sgconfig.yml` at the repository root SHALL register that library as the custom language `haxe` for the extension `hx`. The command SHALL NOT install or build again what the cache already holds for the pin. It SHALL fail when the linked binary does not match a Haxe sample through `sgconfig.yml`. `AGENTS.md` SHALL say when to use `ast-grep`, when Serena and when a text search.

#### Scenario: Fresh worktree
- **WHEN** `tools/setup.sh` is run in a new worktree
- **THEN** `.ast-grep/ast-grep --version` reports the pinned version and `.ast-grep/ast-grep run -p 'throw new $T($$$A)' -l haxe haxe` lists the matching `throw` expressions

#### Scenario: Grammar bump
- **WHEN** the grammar commit in `tools/setup.sh` is changed and the command is run
- **THEN** `.ast-grep/haxe.so` points at the build of the new commit and the build of the old commit is left in place

#### Scenario: Checksum mismatch
- **WHEN** the downloaded `ast-grep` archive does not match the checksum in `tools/setup.sh`
- **THEN** the command fails, names both checksums, and installs nothing

#### Scenario: Broken install in the cache
- **WHEN** the cached binary or grammar library cannot run a Haxe query
- **THEN** the command fails instead of reporting the link
