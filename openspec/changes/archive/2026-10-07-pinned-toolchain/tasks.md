## 1. Compiler
- [x] 1.1 `tools/haxe-build.pin` with the initial build key and checksum
- [x] 1.2 `tools/setup.sh`: download, verify, install per key in the user's cache, link `.haxe`; ignore `.haxe`

## 2. Serena
- [x] 2.1 Build the language server at the fixed commit into the user's cache
- [x] 2.2 Do-nothing backend in `tools/display-backend`; generated display config naming every module
- [x] 2.3 `.serena/project.yml` / `project.local.yml` handling; `.mcp.json`, `.codex/config.toml`

## 3. Rules
- [x] 3.1 `AGENTS.md`: toolchain section, typing check, reference lists not exhaustive
- [x] 3.2 `tools/`, `.mcp.json`, `.codex/` in `.github/infra-paths`

## 4. Verify
- [x] 4.1 Fresh state: one command, `.haxe/haxe --version`, display config exits 0
- [x] 4.2 Serena `find_referencing_symbols` against a text search; `Using --server-connect` in the log
