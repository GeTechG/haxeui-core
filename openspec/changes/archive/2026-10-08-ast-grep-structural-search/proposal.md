## Why
An agent in a checkout of this fork cannot search the code by its shape: `ast-grep` has no Haxe grammar of its own, and the fork neither pins one nor configures it. A text search cannot tell a call from a comment, and Serena answers questions about symbols, not about syntax.

## What Changes
- `tools/setup.sh` installs a pinned `ast-grep` (the prebuilt linux x64 binary from the npm registry archive of `@ast-grep/cli-linux-x64-gnu`, exact version and sha256, downloaded and verified the way the compiler is — no package script runs) and builds the Haxe grammar `GeTechG/tree-sitter-haxe` at a pinned commit with the system C compiler, each into its own per-pin directory of the user's cache, and links both into the gitignored `.ast-grep/`; it ends with a query that proves the binary loads the grammar.
- `sgconfig.yml` at the root registers the grammar as the custom language `haxe` for `*.hx`.
- `AGENTS.md` says when to use `ast-grep`, when Serena and when a text search.
- `sgconfig.yml` becomes an infrastructure path (it does not exist upstream).

Not part of this change: lint rules and a stage in the checks.

## Capabilities

### New Capabilities

### Modified Capabilities
- `toolchain`: the setup command also provides structural search.

## Impact
New: `sgconfig.yml`. Changed: `tools/setup.sh`, `AGENTS.md`, `.github/infra-paths`, `.gitignore`. No library source changes. The setup command additionally needs `cc` and writes to `${XDG_CACHE_HOME:-~/.cache}/ast-grep` and `…/tree-sitter-haxe`.
