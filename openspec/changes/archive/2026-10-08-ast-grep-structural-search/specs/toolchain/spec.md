## ADDED Requirements

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
