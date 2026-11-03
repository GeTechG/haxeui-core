## 1. Pinned CLI and skills
- [x] 1.1 Add `openspec/cli.pin` with `1.16.0`; check: `openspec --version` equals the pin
- [x] 1.2 Generate the skills with `openspec init --tools claude,codex --profile custom` and commit them; check: ten `openspec-*` skills in each of `.claude/skills` and `.agents/skills`, every `generatedBy` equal to the pin
- [x] 1.3 `AGENTS.md`: the pin, how CI runs the CLI, the bump order, `openspec new change` for every new change, `openspec/check.sh` among the checks; check: read against this change's specs

## 2. Validation
- [x] 2.1 `openspec/check.sh` with the five checks of `openspec-tooling`; check: it passes on the branch and fails on a throwaway copy with each defect planted
- [x] 2.2 CI job `openspec` in `.github/workflows/ci.yml` running it at the pinned version; check: the job's commands run green locally with `npm exec` of the pin

## 3. Config rules
- [x] 3.1 `openspec/config.yaml`: `rules.specs`, `rules.tasks`, `operations.apply` and `operations.archive` guidance that refers to `AGENTS.md`; check: `openspec instructions specs --change openspec-pinned-and-validated` shows the rules

## 4. Spec defects
- [x] 4.1 Split the over-long requirements of `button-pointer-states`, `textfield-placeholder` and `toolchain`; check: `openspec validate --all --strict` reports nothing after the sync
