## 1. Setup
- [x] 1.1 `tools/setup.sh`: download the `ast-grep` binary at the pinned version and checksum and build the grammar at the pinned commit into the user's cache; link both into `.ast-grep/` and prove them with a query; ignore `.ast-grep/`
- [x] 1.2 `sgconfig.yml` with the custom language `haxe`; list it in `.github/infra-paths`

## 2. Rules
- [x] 2.1 `AGENTS.md`: when `ast-grep`, when Serena, when a text search

## 3. Verify
- [x] 3.1 Clean worktree: one command, then `throw new $T($$$A)` against a text search, every difference explained
- [x] 3.2 Count of `.hx` files with an `ERROR` node
