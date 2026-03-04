# qibo source map: Simulation Workflows

Generated from source roots:
- `src`
- `tests`
- `examples`

Use this map only after exhausting the topic docs in `doc_map.md`.

## Fast source navigation
- `rg -n "set_backend|get_backend|set_dtype|set_threads" src/qibo/backends/__init__.py`
- `rg -n "def execute|def __call__" src/qibo/models/circuit.py src/qibo/models/evolution.py`
- `rg -n "def frequencies|def samples|class CircuitResult" src/qibo/result.py src/qibo/measurements.py`

## Suggested source entry points
- `src/qibo/backends/__init__.py` | focus: backend and runtime knob selection (`set_backend`, `set_dtype`, `set_threads`) | behavior checks: `tests/test_backends_global.py`
- `src/qibo/backends/abstract.py` | focus: backend interface contract for execution behavior.
- `src/qibo/backends/numpy.py` | focus: baseline simulator execution path.
- `src/qibo/models/circuit.py` | focus: circuit execution path and measurement integration | behavior checks: `tests/test_models_circuit_execution.py`
- `src/qibo/models/evolution.py` | focus: time-evolution execution controls (`execute`, `set_parameters`) | behavior checks: `tests/test_models_evolution.py`
- `src/qibo/models/variational.py` | focus: iterative variational runtime behavior (`QAOA`, `FALQON`) | behavior checks: `tests/test_models_variational.py`
- `src/qibo/measurements.py` | focus: shot accumulation and frequencies/samples conversion | behavior checks: `tests/test_measurements.py`
- `src/qibo/result.py` | focus: state/sample/frequency extraction and metadata persistence | behavior checks: `tests/test_result.py`
- `src/qibo/solvers.py` | focus: solver selection for evolution workflows (`get_solver`).
- `examples/falqon/main.py` | focus: practical iterative runtime controls (`delta_t`, `max_layers`) tied to docs.
