# qibo source map: Developer Guide

Generated from source roots:
- `src`
- `tests`

Use this map only after exhausting the topic docs in `doc_map.md`.

## Fast source navigation
- `rg -n "class Circuit|def execute|def __call__" src/qibo/models/circuit.py`
- `rg -n "class Backend|def construct_backend|def set_backend" src/qibo/backends/abstract.py src/qibo/backends/__init__.py`
- `rg -n "class Passes|restrict_connectivity_qubits" src/qibo/transpiler/pipeline.py`

## Suggested source entry points
- `src/qibo/models/circuit.py` | focus: circuit core execution pipeline and parameter plumbing | behavior checks: `tests/test_models_circuit.py`, `tests/test_models_circuit_execution.py`
- `src/qibo/gates/gates.py` | focus: primitive gate definitions and behavior contracts | behavior checks: `tests/test_gates_gates.py`
- `src/qibo/backends/abstract.py` | focus: backend interface contract for providers | behavior checks: `tests/test_backends.py`
- `src/qibo/backends/__init__.py` | focus: global backend state, backend/transpiler setters/getters | behavior checks: `tests/test_backends_global.py`
- `src/qibo/transpiler/pipeline.py` | focus: pass orchestration and connectivity enforcement | behavior checks: `tests/test_transpiler_pipeline.py`
- `src/qibo/hamiltonians/models.py` | focus: built-in Hamiltonian construction entry points | behavior checks: `tests/test_hamiltonians_models.py`
- `src/qibo/config.py` | focus: error/logging helpers and runtime config settings | behavior checks: `tests/test_backends_global.py`
- `tests/conftest.py` | focus: backend fixture strategy used by the full test suite.
