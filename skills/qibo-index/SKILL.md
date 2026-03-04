---
name: qibo-index
description: Use when users ask how to use Qibo and the request must be routed to the correct topic skill before deeper source inspection.
---

# qibo Skills Index

## Route the request
- Classify the request into one topic skill before giving detailed guidance.
- Keep a docs-first policy: use topic docs/maps first, then source maps.

## Generated topic skills
- `qibo-examples-and-tutorials`: worked examples, tutorial commands, reproduction recipes.
- `qibo-getting-started`: first-run setup, backend basics, first successful circuit execution.
- `qibo-simulation-workflows`: execution lifecycle, sampling/results, runtime tuning.
- `qibo-inputs-and-modeling`: model construction, Hamiltonians, oracles, parameterization.
- `qibo-developer-guide`: architecture, contribution workflow, testing/doc standards.
- `qibo-api-and-scripting`: Python API behavior, circuit/gate usage, model APIs.
- `qibo-build-and-install`: environment bootstrap, dependency resolution, backend install issues.
- `qibo-appendix`: citations/publications and reproducibility metadata capture.

## Topic file map
- `qibo-examples-and-tutorials`: `../qibo-examples-and-tutorials/SKILL.md`, `../qibo-examples-and-tutorials/references/doc_map.md`, `../qibo-examples-and-tutorials/references/source_map.md`
- `qibo-getting-started`: `../qibo-getting-started/SKILL.md`, `../qibo-getting-started/references/doc_map.md`, `../qibo-getting-started/references/source_map.md`
- `qibo-simulation-workflows`: `../qibo-simulation-workflows/SKILL.md`, `../qibo-simulation-workflows/references/doc_map.md`, `../qibo-simulation-workflows/references/source_map.md`
- `qibo-inputs-and-modeling`: `../qibo-inputs-and-modeling/SKILL.md`, `../qibo-inputs-and-modeling/references/doc_map.md`, `../qibo-inputs-and-modeling/references/source_map.md`
- `qibo-developer-guide`: `../qibo-developer-guide/SKILL.md`, `../qibo-developer-guide/references/doc_map.md`, `../qibo-developer-guide/references/source_map.md`
- `qibo-api-and-scripting`: `../qibo-api-and-scripting/SKILL.md`, `../qibo-api-and-scripting/references/doc_map.md`, `../qibo-api-and-scripting/references/source_map.md`
- `qibo-build-and-install`: `../qibo-build-and-install/SKILL.md`, `../qibo-build-and-install/references/doc_map.md`, `../qibo-build-and-install/references/source_map.md`
- `qibo-appendix`: `../qibo-appendix/SKILL.md`, `../qibo-appendix/references/doc_map.md`, `../qibo-appendix/references/source_map.md`

## Preferred simulation start sequence
1. Start with `qibo-build-and-install` if environment is not proven.
2. Move to `qibo-getting-started` for first runnable circuit and backend verification.
3. Route to `qibo-simulation-workflows` or `qibo-inputs-and-modeling` depending on whether the user is execution-first or model-first.
4. Use `qibo-examples-and-tutorials` when a runnable template is faster than writing from scratch.

## Repository roots
- `doc/source`
- `examples`
- `tests`
- `src`
