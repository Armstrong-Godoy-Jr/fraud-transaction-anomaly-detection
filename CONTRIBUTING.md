# Contributing / Git Workflow

This repo follows a lightweight GitFlow-style workflow, scaled for a solo-developed portfolio project but mirroring how a real fraud analytics team would run it.

## Branches

- **`main`** — production branch. Always deployable/demo-ready. Protected: no direct pushes, only merges from `develop` via PR, only when CI passes.
- **`develop`** — integration branch. All phase work lands here first via PR. This is the "current state of the project."
- **`feature/<phase>-<short-description>`** — one branch per unit of work, e.g. `feature/phase0-charter`, `feature/phase3-velocity-features`. Branched from `develop`, merged back into `develop` via PR.

## Workflow per phase

1. `git checkout develop && git pull`
2. `git checkout -b feature/phaseN-short-name`
3. Do the work, commit with Conventional Commits (see below)
4. Push the branch, open a PR into `develop`
5. Self-review against the PR checklist (`.github/PULL_REQUEST_TEMPLATE.md`), confirm CI passes
6. Merge via PR (squash or regular merge, not force-push to shared branches), delete the feature branch
7. When a meaningful milestone is reached (end of a phase, or a few phases), open a PR from `develop` → `main`, merge, then tag a release (see Versioning below)

## Commit Message Convention — Conventional Commits

Format: `<type>(<scope>): <short summary>`

**Types:**
- `feat` — new functionality (a new feature, a new model, a new endpoint)
- `fix` — bug fix
- `docs` — documentation only (README, charter, article drafts)
- `chore` — tooling, scaffolding, dependencies, config
- `refactor` — code change that doesn't add a feature or fix a bug
- `test` — adding/updating tests
- `ci` — CI/workflow changes

**Scope** — use the phase or component, e.g. `phase2`, `features`, `api`, `ci`

**Examples:**
```
feat(phase4): add gradient boosting model with cost-sensitive threshold tuning
docs(phase0): complete project charter
fix(pipeline): correct timezone handling in transaction timestamps
chore(ci): add flake8 line-length config
docs(article): draft Phase 2 EDA section
```

## Versioning

Semantic Versioning (`vMAJOR.MINOR.PATCH`), tagged on `main` at each release point:
- **MAJOR** — a fundamentally different version of the project (rare here)
- **MINOR** — a completed phase or meaningful new capability (e.g. `v0.4.0` after modeling phase lands)
- **PATCH** — a fix or small correction on top of an existing release

Every tag gets an entry in [`CHANGELOG.md`](CHANGELOG.md).

```bash
git tag -a v0.1.0 -m "Repo scaffold + workflow setup"
git push origin v0.1.0
```

## Branch Protection (set once, on GitHub, after first push)

On `main`, under Settings → Branches → Branch protection rules:
- Require a pull request before merging
- Require status checks to pass before merging (CI)
- Do not allow force pushes or deletions
