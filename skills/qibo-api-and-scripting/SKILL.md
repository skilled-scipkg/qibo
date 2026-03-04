---
name: qibo-api-and-scripting
description: This skill should be used when users ask about api and scripting in qibo; it prioritizes documentation references and then source inspection only for unresolved details.
---

# qibo: API and Scripting

## High-Signal Playbook

### Route conditions
- Use this skill for Python API usage, circuit/gate programming patterns, and model-level execution APIs.
- Route to `qibo-getting-started` for first install and first-run setup issues.
- Route to `qibo-simulation-workflows` for backend/runtime tuning and shot-performance tradeoffs.
- Route to `qibo-inputs-and-modeling` for domain-model construction (Grover, qPDF, QAP/QAOA).
- Route to `qibo-examples-and-tutorials` for end-to-end script templates.

### Triage questions
- Is the user building low-level `Circuit` code or using high-level `qibo.models.*` APIs?
- Are they executing statevector-only, measurements-only, or mixed workflows?
- Do they need parameterized training/optimization loops?
- Is backend choice fixed (`numpy`, `qibojit`, `qiboml`) or flexible?
- Do they need transpilation/hardware-target constraints?

### Canonical workflow
1. Identify API layer: `Circuit`/`gates` primitives vs high-level models (`doc/source/api-reference/qibo.rst`).
2. Build a minimal circuit/model with explicit qubit count and gate sequence.
3. Add measurements/registers when shot sampling is required (`doc/source/code-examples/examples.rst`).
4. Execute and inspect outputs via `state()`, `samples()`, and `frequencies()`.
5. For parameterized workflows, update gate/model parameters then re-execute.
6. For optimization loops, use `qibo.optimizers` through model APIs (VQE/QAOA/FALQON).
7. Escalate to source modules only for unresolved behavior details.

### Minimal working example
```python
from qibo import Circuit, gates, set_backend

set_backend("numpy")

c = Circuit(3)
c.add(gates.H(0))
c.add(gates.CNOT(0, 1))
c.add(gates.M(0, 1, 2))

result = c(nshots=200)
print(result.samples(binary=False)[:5])
print(result.frequencies(binary=True))
```

### Pitfalls and fixes
- No measurement outputs: add `gates.M(...)` and pass `nshots` on execution.
- Misread bit order: Qibo uses big-endian qubit order (`doc/source/api-reference/qibo.rst`).
- `Circuit.compile()` expectations: compile path is backend-dependent and mainly relevant for TensorFlow flows (`doc/source/code-examples/examples.rst`).
- Optimizer confusion: `optimize` returns `(best, params, extra)` and methods differ in backend/type expectations (`src/qibo/optimizers.py`).
- Register-level frequency confusion: use `registers=True` for grouped measurement outputs (`doc/source/code-examples/examples.rst`).
- Backend drift: pin backend/dtype at script start for reproducibility.

### Convergence/validation checks
- Circuit sanity: inspect `circuit.summary()` and gate counts before heavy runs.
- Sampling sanity: frequencies sum to `nshots`, and dominant states match circuit intent.
- Parameter update sanity: changing parameters changes observable outputs in expected direction.
- API parity check: small-circuit results agree across at least two backends when available.

## Scope
- Handle questions about language bindings, APIs, and programmatic interfaces.
- Keep responses abstract and architectural for large codebases; avoid exhaustive per-function documentation unless requested.

## Primary documentation references
- `doc/source/api-reference/index.rst`
- `doc/source/api-reference/qibo.rst`
- `doc/source/api-reference/hep.rst`
- `doc/source/code-examples/examples.rst`
- `examples/reuploading_classifier/README.md`

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
- `tests/test_models_circuit.py`
- `tests/test_models_circuit_execution.py`
- `tests/test_result.py`
- `tests/test_models_variational.py`

## Optional deeper inspection
- `src`

## Source entry points for unresolved issues
- `src/qibo/models/circuit.py`
- `src/qibo/gates/gates.py`
- `src/qibo/result.py`
- `src/qibo/measurements.py`
- `src/qibo/models/variational.py`
- `src/qibo/models/encodings.py`
- `src/qibo/optimizers.py`
- `src/qibo/backends/__init__.py`
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" src`).
