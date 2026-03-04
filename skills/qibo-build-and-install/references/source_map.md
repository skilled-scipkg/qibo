# qibo source map: Build and Install

Generated from source roots:
- `src`
- `tests`
- `pyproject.toml`

Use this map only after exhausting the topic docs in `doc_map.md`.

## Fast source navigation
- `rg -n "python =|\[tool.poetry.extras\]|\[tool.poetry.group" pyproject.toml`
- `rg -n "set_backend|get_backend|list_available_backends|construct_backend" src/qibo/backends/__init__.py`
- `rg -n "set_batch_size|set_metropolis_threshold" src/qibo/config.py`

## Suggested source entry points
- `pyproject.toml` | focus: Python constraint, optional backend extras, and test/docs dependency groups.
- `src/qibo/__init__.py` | focus: exported backend/config APIs available immediately after install.
- `src/qibo/backends/__init__.py` | focus: backend discovery and selection (`construct_backend`, `set_backend`, `list_available_backends`).
- `src/qibo/backends/numpy.py` | focus: baseline backend initialization behavior.
- `src/qibo/backends/qulacs.py` | focus: optional backend integration behavior.
- `src/qibo/config.py` | focus: runtime config knobs (`set_batch_size`, `set_metropolis_threshold`).
- `tests/test_backends.py` | behavior checks: backend availability matrix and provider loading.
- `tests/test_backends_global.py` | behavior checks: global backend/dtype/device config state.
- `tests/test_models_circuit_execution.py` | behavior checks: installed package can execute circuits end-to-end.
