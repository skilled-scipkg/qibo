# qibo source map: Getting Started

Generated from source roots:
- `src`
- `tests`

Use this map only after exhausting the topic docs in `doc_map.md`.

## Fast source navigation
- `rg -n "set_backend|get_backend|get_dtype|get_device" src/qibo/backends/__init__.py src/qibo/__init__.py`
- `rg -n "class QFT" src/qibo/models/qft.py`
- `rg -n "class M|def frequencies|def samples" src/qibo/gates/measurements.py src/qibo/result.py`

## Suggested source entry points
- `src/qibo/__init__.py` | focus: import surface for first-run APIs (`Circuit`, backend getters/setters, config utilities).
- `src/qibo/backends/__init__.py` | focus: backend default/selection behavior (`get_backend`, `set_backend`, `set_dtype`).
- `src/qibo/backends/numpy.py` | focus: default simulator backend behavior.
- `src/qibo/models/qft.py` | focus: QFT model entry point used in quickstart smoke tests.
- `src/qibo/models/circuit.py` | focus: `Circuit.execute` and `Circuit.__call__` first-run execution path.
- `src/qibo/gates/measurements.py` | focus: measurement gate `M` behavior for shot-based runs.
- `src/qibo/result.py` | focus: `CircuitResult` extraction (`state`, `samples`, `frequencies`).
- `src/qibo/config.py` | focus: runtime noise/logging knobs (`set_batch_size`, `set_metropolis_threshold`).
- `tests/test_backends_global.py` | behavior checks: backend setup sanity.
- `tests/test_models_circuit_execution.py` | behavior checks: execution and measurement sanity.
- `tests/test_models_qft.py` | behavior checks: QFT smoke behavior.
