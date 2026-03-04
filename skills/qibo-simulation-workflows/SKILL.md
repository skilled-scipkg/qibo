---
name: qibo-simulation-workflows
description: This skill should be used when users ask about simulation workflows in qibo; it prioritizes documentation references and then source inspection only for unresolved details.
---

# qibo: Simulation Workflows

## High-Signal Playbook

### Route conditions
- Use this skill for circuit execution lifecycle, sampling/result handling, and backend/runtime performance tradeoffs.
- Route to `qibo-getting-started` for install/bootstrap issues.
- Route to `qibo-api-and-scripting` for API-shape questions unrelated to runtime behavior.
- Route to `qibo-inputs-and-modeling` for model-construction questions (Hamiltonians, Grover/qPDF/QAOA setup).
- Route to `qibo-examples-and-tutorials` for full runnable scripts and benchmark recipes.

### Triage questions
- Is the target output a final statevector, sampled frequencies, or both?
- What backend is active and what hardware is available (CPU/GPU/multi-GPU)?
- How many qubits and shots are required?
- Are there solver/time-step parameters (`dt`, layers, tolerance) controlling stability?
- Is this a correctness check, a throughput benchmark, or both?

### Canonical workflow
1. Confirm backend policy and default-order behavior (`doc/source/getting-started/backends.rst`).
2. Build or load the circuit/model and decide statevector vs sampling path.
3. Add measurement gates/registers when sampling is required (`doc/source/code-examples/examples.rst`).
4. Execute with explicit runtime knobs (`backend`, `dtype`, `nshots`, device).
5. Inspect outputs through `result.state()`, `result.samples()`, and `result.frequencies()`.
6. Tune runtime knobs (`threads`, device, batch/metropolis thresholds) only after correctness is stable.
7. For iterative models (FALQON/adiabatic), sweep `delta_t`/layers and monitor objective stability.

### Minimal working example
```python
import qibo
from qibo import Circuit, gates

qibo.set_backend("numpy")

c = Circuit(2)
c.add(gates.H(0))
c.add(gates.CNOT(0, 1))
c.add(gates.M(0, 1, register_name="ab"))

result = c(nshots=1000)
print(result.frequencies(binary=True))
print(result.frequencies(binary=True, registers=True))
```

### Pitfalls and fixes
- Missing acceleration despite GPU machine: verify backend package installation and explicit `qibo.set_backend(...)` selection.
- `qibojit` in-place state update surprises workflows that reuse input states; copy states when needed (`doc/source/getting-started/backends.rst`).
- Large shot runs become slow or memory-heavy: tune metropolis threshold/batch size (`doc/source/code-examples/examples.rst`).
- GPU OOM at high qubit counts: move to CPU/distributed strategy or reduce precision (`doc/source/code-examples/advancedexamples.rst`).
- Small circuits slower on GPU: CPU can outperform due to transfer overhead (`doc/source/code-examples/advancedexamples.rst`).
- Measurement-collapse confusion: sampling does not collapse stored final state by default (`doc/source/code-examples/examples.rst`).
- FALQON instability with large `delta_t`: reduce time-step and re-scan layer budget (`examples/falqon/README.md`).

### Convergence/validation checks
- Frequency conservation: total counts equal `nshots`.
- Stability with scale: key observables change smoothly when shots increase.
- Precision check: compare `complex64` vs `complex128` on a reduced instance.
- Backend check: compare a small case across `numpy` and accelerated backend when available.
- Iterative model check: objective (energy/loss) trends are monotonic or bounded as expected.

## Scope
- Handle questions about simulation setup, execution flow, and runtime controls.
- Keep responses abstract and architectural for large codebases; avoid exhaustive per-function documentation unless requested.

## Primary documentation references
- `doc/source/getting-started/backends.rst`
- `doc/source/code-examples/examples.rst`
- `doc/source/code-examples/advancedexamples.rst`
- `examples/qclustering/README.md`
- `examples/shor/README.md`
- `examples/falqon/README.md`
- `examples/benchmarks/results/ADIABATIC.md`
- `examples/benchmarks/results/PRECISION.md`

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
- `tests/test_backends_global.py`
- `tests/test_models_evolution.py`
- `tests/test_models_variational.py`
- `tests/test_result.py`

## Optional deeper inspection
- `src`

## Source entry points for unresolved issues
- `src/qibo/backends/__init__.py`
- `src/qibo/backends/numpy.py`
- `src/qibo/backends/abstract.py`
- `src/qibo/models/circuit.py`
- `src/qibo/models/evolution.py`
- `src/qibo/models/variational.py`
- `src/qibo/result.py`
- `src/qibo/measurements.py`
- `src/qibo/solvers.py`
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" src`).
