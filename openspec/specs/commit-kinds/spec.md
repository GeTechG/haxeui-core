# commit-kinds Specification

## Purpose
Keep every commit either upstreamable code or fork infrastructure, so an upstream PR is a cherry-pick of one task's code commits.

## Requirements

### Requirement: A commit is code or infrastructure, never both
Infrastructure is the set of paths listed in `.github/infra-paths` (paths absent from upstream); every other path is code. CI SHALL reject any non-merge commit that touches both kinds.

#### Scenario: Mixed commit
- **WHEN** a commit changes `haxe/ui/core/Component.hx` and `AGENTS.md`
- **THEN** the `commit-kinds` CI job fails and names the commit

#### Scenario: Single-kind commit
- **WHEN** a commit changes only code paths, or only infrastructure paths
- **THEN** the check passes

### Requirement: The check proves itself
`.github/scripts/check-commit-kinds-test.sh` SHALL build a throwaway repository with a mixed commit and fail unless the check rejects it; CI runs it before the real check.

#### Scenario: Check that accepts a mixed commit
- **WHEN** `check-commit-kinds.sh` exits 0 on the throwaway repository's mixed commit
- **THEN** the self-test prints `FAIL: mixed commit accepted` and exits non-zero

#### Scenario: Working check
- **WHEN** the check passes the throwaway repository's code-only and infrastructure-only commits and rejects its mixed commit
- **THEN** the self-test prints `ok` and exits 0
