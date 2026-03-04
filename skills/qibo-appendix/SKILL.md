---
name: qibo-appendix
description: Use when users ask for Qibo citation guidance, publication references, or reproducibility metadata to include with simulation results.
---

# qibo: Appendix

## High-Signal Playbook

### Route conditions
- Use this skill for citation policy, bibliography questions, and reproducibility metadata capture.
- Route to `qibo-getting-started` or `qibo-build-and-install` for install/runtime failures.
- Route to `qibo-api-and-scripting` or `qibo-simulation-workflows` when the request becomes implementation/performance focused.

### Triage questions
- Does the user need publication citations, thesis references, or collaboration references?
- Do they need reproducibility metadata (Qibo version/backend/dtype/device) for methods sections?
- Are they citing a specific simulation result artifact?

### Canonical workflow
1. Start from `doc/source/appendix/citing-qibo.rst` for official citation guidance.
2. If needed, include repository citation pointers from `README.md`.
3. Collect reproducibility metadata from a live environment (`qibo.__version__`, backend, dtype, device).
4. If metadata formatting is unclear, inspect source entry points in `references/source_map.md`.

### Minimal working example
```bash
python - <<'PY'
import qibo
print("qibo_version:", qibo.__version__)
print("backend:", qibo.get_backend())
print("dtype:", qibo.get_dtype())
print("device:", qibo.get_device())
print("available_backends:", qibo.list_available_backends())
PY
```

### Pitfalls and fixes
- Citing only package name is incomplete for papers; include references from `doc/source/appendix/citing-qibo.rst`.
- Reproducibility sections often omit runtime/backend details; always record backend, dtype, and device.
- Optional backend availability differs by environment; include the output of `qibo.list_available_backends()` when relevant.

### Convergence/validation checks
- Citation text maps directly to entries in `doc/source/appendix/citing-qibo.rst`.
- Reproducibility block contains version, backend, dtype, and device.
- Metadata command runs successfully in the same environment used for simulations.

## Scope
- Handle questions about appendix/citation documentation and reproducibility metadata.
- Keep responses concise and traceable to repository paths.

## Primary documentation references
- `doc/source/appendix/citing-qibo.rst`
- `README.md`

## Workflow
- Start with the primary references above.
- If details are missing, inspect `references/doc_map.md` for additional context.
- If ambiguity remains after docs, inspect `references/source_map.md` for implementation details behind metadata fields.
- Cite exact file paths in responses.

## Tutorials and examples
- `examples`

## Test references
- `tests/test_models_circuit.py`
- `tests/test_models_circuit_qasm.py`
- `tests/test_backends_global.py`

## Optional deeper inspection
- `src`

## Source entry points for unresolved issues
- `src/qibo/__init__.py`
- `src/qibo/backends/__init__.py`
- `src/qibo/backends/abstract.py`
- `src/qibo/result.py`
- `src/qibo/config.py`
- Prefer targeted source search (for example: `rg -n "__version__|versions|get_backend|get_dtype|get_device" src/qibo`).
