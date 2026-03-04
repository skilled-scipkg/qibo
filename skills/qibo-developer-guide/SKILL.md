---
name: qibo-developer-guide
description: This skill should be used when users ask about developer guide in qibo; it prioritizes documentation references and then source inspection only for unresolved details.
---

# qibo: Developer Guide

## High-Signal Playbook

### Route conditions
- Use this skill for architecture orientation, contribution workflow, testing standards, and docs contribution process.
- Route to `qibo-build-and-install` for dependency/bootstrap failures before development starts.
- Route to `qibo-api-and-scripting` for end-user API usage questions.
- Route to `qibo-simulation-workflows` for runtime behavior/performance troubleshooting.
- Route to `qibo-inputs-and-modeling` for domain-model logic questions.

### Triage questions
- Is the change a bug fix, feature addition, backend extension, or docs update?
- Which subsystem is impacted (gates, models, backends, transpiler, UI, hamiltonians)?
- Does the change alter public API behavior or numerical defaults?
- What tests cover the change, and do new tests need to be added?
- Are docs/examples affected and updated in the same change set?

### Canonical workflow
1. Locate component boundaries via `doc/source/developer-guides/general.rst` and relevant `src/qibo` modules.
2. Create a minimal failing or target behavior test in `tests/` first.
3. Implement source changes in the narrowest module scope.
4. Run targeted tests, then broader regression suites.
5. Run lint/pre-commit checks.
6. Update docs/docstrings and build docs locally (`doc/source`, `make -C doc html`).
7. Prepare PR with behavior summary, test evidence, and migration notes if API changed.

### Minimal working example
```bash
pytest tests/test_models_circuit.py -k measurement
pytest tests/test_backends_global.py
pre-commit run --all-files
make -C doc html
```

### Pitfalls and fixes
- Developer docs reference legacy paths like `qibo/tests`; in this repo tests live under `tests/`.
- Skipping tests for backend-sensitive changes causes regressions; run at least one backend-focused suite (`tests/test_backends.py`, `tests/test_backends_global.py`).
- Missing docstring/docs updates for public APIs desynchronizes Sphinx output; update `doc/source` links and docstrings together.
- Printing directly instead of logging can violate project checks; use configured logging utilities (`qibo.config`).
- Transpiler/backend changes without connectivity/native-gate assertions can break hardware flows (`src/qibo/transpiler/pipeline.py`).
- Optional backend dependencies (qulacs/qbraid/qibojit) may not be present in all environments; guard tests/features accordingly.

### Convergence/validation checks
- Targeted tests for modified subsystem pass locally.
- Wider `pytest` run remains green with no unexpected failures.
- Lint/pre-commit checks pass.
- Docs build succeeds and rendered pages include updated symbols.
- If behavior changed, add or update regression tests in `tests/regressions/` where applicable.

## Scope
- Handle questions about developer architecture, extension points, and contribution workflow.
- Keep responses abstract and architectural for large codebases; avoid exhaustive per-function documentation unless requested.

## Primary documentation references
- `doc/source/developer-guides/index.rst`
- `doc/source/developer-guides/general.rst`
- `doc/source/developer-guides/contributing.rst`
- `doc/source/index.rst`
- `pyproject.toml`

## Workflow
- Start with the primary references above.
- If details are missing, inspect `references/doc_map.md` for the complete topic document list.
- Use tutorials/examples as executable usage patterns when available.
- Use tests as behavior or regression references when available.
- If ambiguity remains after docs, inspect `references/source_map.md` and start with the ranked source entry points.
- Cite exact documentation file paths in responses.

## Tutorials and examples
- `examples`

## Test references
- `tests`

## Optional deeper inspection
- `src`

## Source entry points for unresolved issues
- `src/qibo/models/circuit.py`
- `src/qibo/gates/gates.py`
- `src/qibo/backends/abstract.py`
- `src/qibo/backends/__init__.py`
- `src/qibo/transpiler/pipeline.py`
- `src/qibo/hamiltonians/models.py`
- `src/qibo/config.py`
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" src tests`).
