---
name: qibo-getting-started
description: This skill should be used when users ask about getting started in qibo; it prioritizes documentation references and then source inspection only for unresolved details.
---

# qibo: Getting Started

## High-Signal Playbook

### Route conditions
- Use this skill for first-run setup, backend selection basics, and the first successful circuit execution.
- Route to `qibo-build-and-install` for environment packaging failures (`pip`/`conda`, dependency resolution, extras).
- Route to `qibo-simulation-workflows` for runtime tuning, sampling strategy, and performance debugging.
- Route to `qibo-api-and-scripting` for deeper API design questions beyond initial setup.
- Route to `qibo-examples-and-tutorials` when the user asks for domain-specific tutorials or benchmark scripts.

### Triage questions
- What Python version and environment manager are being used (`venv`, `conda`, system)?
- Is the user targeting base CPU simulation or optional accelerated backends (`qibojit`, `qiboml`)?
- Does the user need statevector output, shot-based measurements, or both?
- Are there import-time warnings about backend availability or performance?
- Is this a smoke test install check or the start of a larger workflow?

### Canonical workflow
1. Confirm version constraints and install path (`doc/source/getting-started/installation.rst`, `pyproject.toml`).
2. Install base package (`pip install qibo`) or conda equivalent (`doc/source/getting-started/quickstart.rst`).
3. If needed, install optional backends and set explicitly with `qibo.set_backend(...)` (`doc/source/getting-started/backends.rst`).
4. Verify active backend/dtype (`qibo.get_backend()`, `qibo.get_dtype()`).
5. Run a minimal QFT circuit to validate statevector execution (`doc/source/getting-started/quickstart.rst`, `README.md`).
6. Run a measurement circuit with `gates.M(...)` and `nshots` to validate sampling path.
7. If logs/warnings block interpretation, control verbosity via `QIBO_LOG_LEVEL` (`doc/source/getting-started/backends.rst`).

### Minimal working example
```python
import qibo
from qibo import Circuit, gates
from qibo.models import QFT

qibo.set_backend("numpy")
qft = QFT(5)
state = qft().state()

c = Circuit(2)
c.add(gates.X(0))
c.add(gates.M(0, 1))
result = c(nshots=100)

print(qibo.get_backend(), qibo.get_dtype(), len(state))
print(result.frequencies(binary=True))
```

### Pitfalls and fixes
- Python version mismatch: docs mention `>=3.8/3.9`, but this repo currently pins `>=3.10,<3.14` in `pyproject.toml`; align environment first.
- Import warning about missing `qibojit`: base install still works, but install `qibojit` for better performance (`doc/source/getting-started/backends.rst`).
- GPU acceleration not active after `qibojit` install: install `cupy` (and optional `cuQuantum`) as noted in `doc/source/getting-started/installation.rst`.
- Empty/unchanged frequencies: ensure measurement gates were added and `nshots` passed.
- Noisy startup logs: use `QIBO_LOG_LEVEL=3` to hide info or `QIBO_LOG_LEVEL=4` to hide info and warnings.
- Unexpected backend selection across sessions: set backend explicitly at script start.

### Convergence/validation checks
- Backend check: `qibo.get_backend()` and device match expected runtime.
- Result consistency: frequencies sum exactly to `nshots`.
- Smoke-test sanity: deterministic circuits produce the expected dominant bitstring.
- State sanity: final state has expected length `2**nqubits` and norm close to 1.

## Scope
- Handle questions about initial setup, quickstarts, and core concepts.
- Keep responses abstract and architectural for large codebases; avoid exhaustive per-function documentation unless requested.

## Primary documentation references
- `doc/source/getting-started/index.rst`
- `doc/source/getting-started/overview.rst`
- `doc/source/getting-started/quickstart.rst`
- `doc/source/getting-started/backends.rst`
- `doc/source/getting-started/installation.rst`
- `README.md`

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
- `tests/test_models_circuit_execution.py`
- `tests/test_models_qft.py`

## Optional deeper inspection
- `src`

## Source entry points for unresolved issues
- `src/qibo/__init__.py`
- `src/qibo/backends/__init__.py`
- `src/qibo/backends/numpy.py`
- `src/qibo/models/circuit.py`
- `src/qibo/models/qft.py`
- `src/qibo/result.py`
- `src/qibo/config.py`
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" src`).
