---
name: qibo-examples-and-tutorials
description: This skill should be used when users ask about examples and tutorials in qibo; it prioritizes documentation references and then source inspection only for unresolved details.
---

# qibo: Examples and Tutorials

## High-Signal Playbook

### Route conditions
- Use this skill to map user goals to runnable example folders and reproducible command patterns.
- Route to `qibo-getting-started` if installation/backend bootstrap is unresolved.
- Route to `qibo-simulation-workflows` for runtime tuning and result-interpretation issues.
- Route to `qibo-inputs-and-modeling` for model formulation questions hidden behind an example script.
- Route to `qibo-api-and-scripting` for reusable API extraction after prototyping with examples.

### Triage questions
- What problem class is targeted (optimization, Grover, finance, clustering, HEP, etc.)?
- Is the user asking for a quick smoke test or full paper-level reproduction?
- Are optional dependencies or external datasets required?
- What runtime budget and hardware are available?
- Does the user need notebook-style or pure script/CLI execution?

### Canonical workflow
1. Map goal to topic/algorithm index (`doc/source/code-examples/applications-by-topic.rst`, `applications-by-algorithm.rst`).
2. Pick the smallest matching example from `examples/README.md`.
3. Verify prerequisites (backend package, extra libraries, external data files).
4. Run from the example directory using README/test-backed arguments.
5. Validate outputs against README-described artifacts/metrics.
6. Shrink or scale parameters to fit runtime budget.
7. Promote stable pattern into a standalone script/API workflow.

### Minimal working example
```bash
cd examples/reuploading_classifier
python main.py --dataset circle --layers 2
```

```bash
cd examples/qclustering
python train_qkmedians.py --train_size 600 --read_file data/latentrep_QCD_sig.h5 --k 2 --seed 123 --tolerance 1e-3 --min_type classic --save_dir output_dir --verbose true --nprint 1
```

### Pitfalls and fixes
- Running from repository root instead of example folder breaks relative paths; `cd` into each example directory first.
- Missing extras for specific examples (for example `h5py` in `examples/qclustering/README.md`); install before execution.
- External dataset not downloaded (qclustering); fetch data before training/evaluation.
- Long default runs in some tutorials (for example large random-state counts); start with smaller parameters (`examples/3_tangle/README.md`).
- Memory warnings from dense symbolic Hamiltonians in optimization examples; switch to smaller instances or sparse/symbolic setup (`examples/qap/README.md`, `examples/mvc/README.md`).
- Backend assumption mismatch: some scripts assume `qibojit` defaults; set backend explicitly when needed.

### Convergence/validation checks
- Smoke-test first: run reduced-size arguments that mirror `examples/test_examples.py` patterns.
- Metric check: confirm expected artifacts (frequencies, ROC plots, printed factors/errors) are produced.
- Reproducibility: pin seed-related flags where offered by the example.
- Scaling check: increase qubits/layers/shots gradually and verify qualitative behavior remains consistent.

## Scope
- Handle questions about worked examples, tutorials, and cookbook usage.
- Keep responses abstract and architectural for large codebases; avoid exhaustive per-function documentation unless requested.

## Primary documentation references
- `examples/README.md`
- `doc/source/code-examples/index.rst`
- `doc/source/code-examples/applications.rst`
- `doc/source/code-examples/applications-by-topic.rst`
- `doc/source/code-examples/applications-by-algorithm.rst`
- `examples/mvc/README.md`
- `examples/unary/README.md`
- `examples/3_tangle/README.md`
- `examples/benchmarks/results/HARDWARE.md`
- `examples/benchmarks/results/QFT.md`
- `examples/benchmarks/results/SHOTS.md`
- `examples/benchmarks/results/VAR5.md`

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
- `examples/test_examples.py`

## Optional deeper inspection
- `src`

## Source entry points for unresolved issues
- `examples/test_examples.py`
- `examples/grover/example1.py`
- `examples/falqon/main.py`
- `examples/qclustering/train_qkmedians.py`
- `src/qibo/models/grover.py`
- `src/qibo/models/variational.py`
- `src/qibo/models/qft.py`
- `src/qibo/quantum_info/entanglement.py`
- `src/qibo/result.py`
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" src examples`).
