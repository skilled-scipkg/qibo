# qibo source map: Inputs and Modeling

Generated from source roots:
- `src`
- `tests`

Use this map only after exhausting the topic docs in `doc_map.md`.

## Fast source navigation
- `rg -n "class Grover|def execute|def __call__" src/qibo/models/grover.py`
- `rg -n "class qPDF|def predict|def qpdf_hamiltonian" src/qibo/models/hep.py`
- `rg -n "def TFIM|def MaxCut|def Heisenberg" src/qibo/hamiltonians/models.py`

## Suggested source entry points
- `src/qibo/models/grover.py` | focus: Grover iteration setup, oracle handling, execution behavior | behavior checks: `tests/test_models_grover.py`
- `src/qibo/models/hep.py` | focus: qPDF model parameterization and prediction path | behavior checks: `tests/test_models_hep.py`
- `src/qibo/hamiltonians/models.py` | focus: built-in Hamiltonian constructors for model inputs | behavior checks: `tests/test_hamiltonians_models.py`
- `src/qibo/models/evolution.py` | focus: `StateEvolution` and `AdiabaticEvolution` parameter/runtime behavior | behavior checks: `tests/test_models_evolution.py`
- `src/qibo/models/variational.py` | focus: variational model update loops (`VQE`, `QAOA`, `AAVQE`, `FALQON`) | behavior checks: `tests/test_models_variational.py`
- `src/qibo/models/encodings.py` | focus: feature/state encoders used by modeling workflows | behavior checks: `tests/test_models_encodings.py`
- `src/qibo/models/iqae.py` | focus: iterative amplitude estimation workflow | behavior checks: `tests/test_models_iqae.py`
- `src/qibo/models/circuit.py` | focus: circuit container used as modeling substrate.
