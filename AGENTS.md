# haxeui-core — agent guide

Independent fork of `haxeui/haxeui-core` (the core library of HaxeUI). Its consumers pin it by commit; they do not dictate how it is worked on. This file is the source of truth here.

## Branches and delivery
- One task — one branch, cut from `master`.
- Delivery is a PR to `master`; never push to `master` directly.

## Commits
- Every commit is **code** (library sources and tests: `haxe/`, `cli/`, upstream metadata) or **infrastructure** (the paths listed in `.github/infra-paths`: this file, `openspec/`, our CI and scripts). Never both — CI rejects a mixed commit.
- OpenSpec artifacts (proposal, tasks, specs, archive) are infrastructure: they never share a commit with code.
- Code commit messages are written as for upstream: `area(scope): imperative summary`, no mention of consumers or their paths.
- An upstream PR is a cherry-pick of one task's code commits; keep them self-contained.
- Changing the list of infrastructure paths is an infrastructure commit.

## Checks
Run before pushing:
- `bash .github/scripts/check-commit-kinds-test.sh` — self-test of the commit-kind check.
- `bash .github/scripts/check-commit-kinds.sh origin/master..HEAD` — the check on your branch.

The library has no test suite or standalone build of its own (it compiles only with a backend); a code change is verified by compiling a backend against it, e.g. the `build` job of `GeTechG/haxeui-heaps`.

## Specs
`openspec/` holds this fork's own specs (`openspec/specs/`). Behaviour or rule changes go through `openspec/changes/`.
