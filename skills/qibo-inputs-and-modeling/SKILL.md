---
name: qibo-inputs-and-modeling
description: This skill should be used when users ask about inputs and modeling in qibo; it prioritizes documentation references and then source inspection only for unresolved details.
---

# qibo: Inputs and Modeling

## High-Signal Playbook

### Route conditions
- Use this skill for problem encoding, model construction, Hamiltonian setup, and parameterization strategy.
- Route to `qibo-simulation-workflows` for execution/runtime optimization after model construction.
- Route to `qibo-api-and-scripting` for low-level API syntax and reusable coding patterns.
- Route to `qibo-examples-and-tutorials` for full scripts/notebooks tied to a specific domain task.
- Route to `qibo-developer-guide` when extending model internals rather than using existing APIs.

### Triage questions
- Which model family is needed (Grover/search, variational optimization, adiabatic evolution, qPDF/HEP, encodings)?
- What is the input representation (graph, matrix file, oracle circuit, feature vector/grid)?
- Are constraints/feasibility checks required (QAP/MVC-like formulations)?
- Is dense or symbolic Hamiltonian representation acceptable for memory budget?
- Is the number of solutions/target amplitude known (relevant for Grover mode)?
- Are backend precision and optimizer choices fixed?

### Canonical workflow
1. Classify the modeling objective and select the minimal matching API (`doc/source/api-reference/qibo.rst`, `doc/source/api-reference/hep.rst`).
2. Validate and load inputs (for example QAP matrix/oracle circuit/x-grid).
3. Build circuit/model objects (`Grover`, `QAOA`, `StateEvolution`, `qPDF`, encoders).
4. Choose Hamiltonian representation (`dense` vs symbolic) and backend.
5. Run a reduced-size baseline to validate feasibility and outputs.
6. Add optimization or iterative control parameters only after baseline correctness.
7. Validate solution quality with feasibility checks, expectation trends, and sensitivity scans.

### Minimal working example
```python
from qibo import Circuit, gates
from qibo.models.grover import Grover

oracle = Circuit(6)
oracle.add(gates.X(5).controlled_by(*range(5)))

grover = Grover(oracle, superposition_qubits=5, number_solutions=1)
solution, iterations = grover()
print(solution, iterations)
```

```python
import numpy as np
from qibo.models.hep import qPDF

model = qPDF(ansatz="Weighted", layers=1, nqubits=2)
params = np.zeros(model.nparams)
x = np.array([0.1, 0.2, 0.4])
print(model.predict(params, x))
```

### Pitfalls and fixes
- Grover ancilla/superposition mismatch: set `superposition_qubits` when oracle uses ancillas (`examples/grover/README.md`, `src/qibo/models/grover.py`).
- QAP random assignments often infeasible: run explicit feasibility checks before energy comparison (`examples/qap/README.md`).
- Dense symbolic Hamiltonian expansion is memory expensive; keep symbolic/smaller systems when possible (`examples/qap/README.md`, `examples/mvc/README.md`).
- Adiabatic/AAVQE scheduling functions must satisfy boundary constraints (`s(0)=0`, `s(1)=1`) (`src/qibo/models/evolution.py`, `src/qibo/models/variational.py`).
- qPDF parameter length mismatch causes runtime errors; enforce `len(parameters) == model.nparams` (`src/qibo/models/hep.py`).
- Overly large combinatorial instances can exceed practical QAOA limits; reduce instance size for baseline validation first (`examples/qap/README.md`).

### Convergence/validation checks
- Feasibility first: candidate combinatorial solutions satisfy all constraints before ranking energies.
- Objective trend: optimized energy/score improves across iterations or restarts.
- Small-instance parity: dense vs symbolic or alternate solver choices agree on reduced systems.
- Grover validation: returned bitstrings satisfy domain `check` predicate when available.
- qPDF sanity: outputs are finite across target `x` grid and stable under small parameter perturbations.

## Scope
- Handle questions about inputs, system setup, models, and physical parameterization.
- Keep responses abstract and architectural for large codebases; avoid exhaustive per-function documentation unless requested.

## Primary documentation references
- `doc/source/api-reference/qibo.rst`
- `doc/source/api-reference/hep.rst`
- `doc/source/code-examples/advancedexamples.rst`
- `examples/grover/README.md`
- `examples/qap/README.md`
- `examples/qPDF/qPDF.ipynb`

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
- `tests/test_models_grover.py`
- `tests/test_models_hep.py`
- `tests/test_hamiltonians_models.py`
- `tests/test_models_encodings.py`

## Optional deeper inspection
- `src`

## Source entry points for unresolved issues
- `src/qibo/models/grover.py`
- `src/qibo/models/hep.py`
- `src/qibo/hamiltonians/models.py`
- `src/qibo/models/evolution.py`
- `src/qibo/models/variational.py`
- `src/qibo/models/encodings.py`
- `src/qibo/models/iqae.py`
- `src/qibo/models/circuit.py`
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" src`).
