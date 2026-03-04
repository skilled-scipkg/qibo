---
name: qibo-build-and-install
description: Use when users need Qibo installation, environment setup, optional backend dependency setup, or local source builds before running simulations.
---

# qibo: Build and Install

## High-Signal Playbook

### Route conditions
- Use this skill for package installation, Python/toolchain compatibility checks, and backend dependency troubleshooting.
- Route to `qibo-getting-started` once install is complete and the user needs first-circuit execution help.
- Route to `qibo-simulation-workflows` for runtime tuning/performance after environment bootstrap.
- Route to `qibo-developer-guide` for contribution workflow and CI/lint/doc commands.

### Triage questions
- Is the user installing from PyPI (`pip install qibo`) or from local source (`pip install .`)?
- What Python version is active, and does it satisfy `pyproject.toml` (`>=3.10,<3.14`)?
- Are optional backends required (`qibojit`, `qiboml`, `qulacs`, qir/cudaq extras)?
- Is the goal a quick runtime smoke test or full developer setup with tests/docs tooling?

### Canonical workflow
1. Verify Python version and package constraints from `pyproject.toml`.
2. Create a clean virtual environment and upgrade `pip`.
3. Install Qibo (`pip install qibo` or `pip install .` from repository root).
4. Install optional backend packages if needed (`qibojit`, `qiboml`, `qulacs`, extras in `pyproject.toml`).
5. Verify backend availability with `qibo.list_available_backends()`.
6. Run a minimal circuit smoke test.
7. Run one backend test for confidence (`tests/test_backends_global.py`).

### Minimal working example
```bash
python -m venv .venv
source .venv/bin/activate
python -m pip install -U pip
python -m pip install .
```

```bash
python - <<'PY'
import qibo
from qibo.models import QFT

qibo.set_backend("numpy")
state = QFT(4)().state()
print("version:", qibo.__version__)
print("backend:", qibo.get_backend())
print("state_len:", len(state))
print("available:", qibo.list_available_backends())
PY
```

```bash
pytest tests/test_backends_global.py -k set_get_backend
```

### Pitfalls and fixes
- Docs mention Python `>=3.9` while this repository enforces `>=3.10,<3.14` in `pyproject.toml`; follow the repository constraint.
- Missing optional backend package causes backend selection/import warnings; install the matching package before calling `qibo.set_backend(...)`.
- GPU acceleration with `qibojit` also needs `cupy` (and optional `cuQuantum`) as described in `doc/source/getting-started/installation.rst`.
- Backend discovery mismatch after reinstall can come from mixed environments; recreate a clean virtual environment.

### Convergence/validation checks
- `import qibo` succeeds with no hard import errors.
- `qibo.list_available_backends()` includes expected providers.
- A small QFT/circuit run returns a valid state/result object.
- Targeted backend smoke test passes.

## Scope
- Handle questions about build, installation, compilation, and environment setup.
- Keep responses practical and execution-oriented, with explicit commands and validation checks.

## Primary documentation references
- `doc/source/getting-started/installation.rst`
- `doc/source/getting-started/backends.rst`
- `doc/source/getting-started/quickstart.rst`
- `README.md`
- `pyproject.toml`

## Workflow
- Start with the primary references above.
- If details are missing, inspect `references/doc_map.md` for additional topic docs.
- Use tests as behavior checks for setup correctness.
- If ambiguity remains after docs, inspect `references/source_map.md` and start with the ranked source entry points.
- Cite exact file paths in responses.

## Tutorials and examples
- `examples`

## Test references
- `tests/test_backends.py`
- `tests/test_backends_global.py`
- `tests/test_models_circuit_execution.py`

## Optional deeper inspection
- `src`

## Source entry points for unresolved issues
- `src/qibo/__init__.py`
- `src/qibo/backends/__init__.py`
- `src/qibo/backends/numpy.py`
- `src/qibo/backends/qulacs.py`
- `src/qibo/config.py`
- Prefer targeted source search (for example: `rg -n "set_backend|list_available_backends|construct_backend" src/qibo/backends src/qibo/config.py`).
