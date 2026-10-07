## Why
The fork does not say which compiler builds it, and Serena is not wired in it: an agent types the code with whatever Haxe 4.x the system has and works without symbol navigation.

## What Changes
- The compiler is pinned in the repository (`tools/haxe-build.pin`: build key and archive checksum of a `GeTechG/haxe` build) and installed by one command per checkout, `tools/setup.sh`, behind the gitignored `.haxe` link.
- The same command builds a Haxe 5 capable language server, generates a display config that types the library against a do-nothing backend (`tools/display-backend`) and names every module, and points Serena at both. Serena is registered for Claude Code (`.mcp.json`) and Codex (`.codex/config.toml`).
- `AGENTS.md` gains the rule: build, type and test only with the pinned compiler; language-server reference lists are not exhaustive.
- `tools/`, `.mcp.json` and `.codex/` become infrastructure paths (they do not exist upstream).

## Capabilities

### New Capabilities
- `toolchain`: the pinned compiler, the per-checkout setup command, and the Serena wiring.

### Modified Capabilities

## Impact
New: `tools/`, `.mcp.json`, `.codex/config.toml`. Changed: `AGENTS.md`, `.github/infra-paths`, `.gitignore`. No library source changes. The setup command needs network access on first use and writes to `${XDG_CACHE_HOME:-~/.cache}/haxe-build` and `…/haxe-language-server`.
