# qibo source map: API and Scripting

Generated from source roots:
- `src`
- `tests`

Use this map only after exhausting the topic docs in `doc_map.md`.

## Fast source navigation
- `rg -n "class Circuit|def execute|def __call__" src/qibo/models/circuit.py`
- `rg -n "class CircuitResult|def frequencies|def samples|def state" src/qibo/result.py src/qibo/measurements.py`
- `rg -n "def optimize|class VQE|class QAOA|class FALQON" src/qibo/optimizers.py src/qibo/models/variational.py`

## Suggested source entry points
- `src/qibo/models/circuit.py` | focus: `Circuit.add`, `Circuit.set_parameters`, `Circuit.execute`, `Circuit.__call__` | behavior checks: `tests/test_models_circuit.py`, `tests/test_models_circuit_execution.py`
- `src/qibo/gates/gates.py` | focus: core gate classes and parametrized gate behavior | behavior checks: `tests/test_gates_gates.py`
- `src/qibo/measurements.py` | focus: `MeasurementResult`, `frequencies_to_binary`, `apply_bitflips` | behavior checks: `tests/test_measurements.py`, `tests/test_measurements_probabilistic.py`
- `src/qibo/result.py` | focus: `load_result`, `CircuitResult`, frequency/sample/state APIs | behavior checks: `tests/test_result.py`
- `src/qibo/optimizers.py` | focus: `optimize`, `newtonian`, `sgd` dispatch logic | behavior checks: `tests/test_models_variational.py`
- `src/qibo/models/variational.py` | focus: `VQE`, `QAOA`, `FALQON` execution/update logic | behavior checks: `tests/test_models_variational.py`
- `src/qibo/backends/__init__.py` | focus: `set_backend`, `get_backend`, `set_dtype`, backend construction | behavior checks: `tests/test_backends_global.py`
- `src/qibo/parameter.py` | focus: parameter object update/evaluation plumbing | behavior checks: `tests/test_parameter.py`
