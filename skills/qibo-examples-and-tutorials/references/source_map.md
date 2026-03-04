# qibo source map: Examples and Tutorials

Generated from source roots:
- `examples`
- `src`
- `tests`

Use this map only after exhausting the topic docs in `doc_map.md`.

## Fast source navigation
- `rg -n "def main\(" examples/*/main.py examples/grover/example*.py`
- `rg -n "def test_" examples/test_examples.py`
- `rg -n "class Grover|class FALQON|class QAOA|class StateEvolution" src/qibo/models`

## Suggested source entry points
- `examples/test_examples.py` | focus: runnable smoke-test arguments and expected execution patterns across examples.
- `examples/reuploading_classifier/main.py` | focus: compact train/eval loop and CLI argument defaults.
- `examples/grover/example1.py` | focus: minimal Grover usage pattern and oracle sizing.
- `examples/falqon/main.py` | focus: iterative variational loop (`delta_t`, `max_layers`) behavior.
- `examples/shor/main.py` | focus: multi-stage algorithm flow and run controls.
- `examples/qclustering/train_qkmedians.py` | focus: data-file input path and clustering run settings.
- `src/qibo/models/grover.py` | focus: Grover execution internals behind example scripts | behavior checks: `tests/test_models_grover.py`
- `src/qibo/models/variational.py` | focus: VQE/QAOA/FALQON model internals used by optimization examples | behavior checks: `tests/test_models_variational.py`
- `src/qibo/models/evolution.py` | focus: adiabatic/state-evolution execution internals | behavior checks: `tests/test_models_evolution.py`
- `src/qibo/models/qft.py` | focus: QFT model behavior used in benchmark/tutorial scripts | behavior checks: `tests/test_models_qft.py`
- `src/qibo/result.py` | focus: output extraction helpers (`state`, `samples`, `frequencies`) used by examples | behavior checks: `tests/test_result.py`
