# qibo source map: Appendix

Generated from source roots:
- `src`
- `tests`

Use this map only after exhausting the topic docs in `doc_map.md`.

## Fast source navigation
- `rg -n "__version__|versions" src/qibo`
- `rg -n "get_backend|get_dtype|get_device|list_available_backends" src/qibo/backends src/qibo/__init__.py`

## Suggested source entry points
- `src/qibo/__init__.py` | focus: package version export (`__version__`) and public API exports | behavior checks: `tests/test_models_circuit.py`, `tests/test_models_circuit_qasm.py`
- `src/qibo/backends/abstract.py` | focus: backend `versions` metadata for reproducibility records | behavior checks: `tests/test_backends.py`
- `src/qibo/backends/__init__.py` | focus: `get_backend`, `get_dtype`, `get_device`, `list_available_backends` | behavior checks: `tests/test_backends_global.py`
- `src/qibo/result.py` | focus: result metadata fields persisted in saved states/results | behavior checks: `tests/test_result.py`
- `src/qibo/config.py` | focus: logger formatting/version-aware runtime metadata | behavior checks: `tests/test_backends_global.py`
