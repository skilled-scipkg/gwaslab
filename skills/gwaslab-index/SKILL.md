---
name: gwaslab-index
description: Use this router for GWASLab requests; select the most specific topic skill first, stay docs-first, and escalate to source inspection only when documentation cannot resolve behavior details.
---

# gwaslab Skills Index

## Deterministic Routing Order
1. Installation or environment setup -> `gwaslab-build-and-install`
2. First-run onboarding and quick analysis -> `gwaslab-getting-started`
3. API/CLI programming patterns and automation -> `gwaslab-api-and-scripting`
4. Input schema mapping and format conversion -> `gwaslab-inputs-and-modeling`
5. QC, harmonization, clumping, downstream pipelines -> `gwaslab-simulation-workflows`
6. Plotting, reporting, and output artifact tuning -> `gwaslab-analysis-and-output`
7. "Show me an example" or notebook/script adaptation -> `gwaslab-examples-and-tutorials`
8. Failure diagnosis and edge-case handling -> `gwaslab-troubleshooting`
9. Specialized single-doc/reference-data topics (VCF/FASTA/GTF/reference downloads, reserved headers, ancestry, update logs, theory, utility docs) -> `gwaslab-advanced-topics`
10. Parallel/HPC execution questions -> `gwaslab-parallel-hpc`

## Escalation Rule (Docs -> Source)
1. Start from the selected skill `SKILL.md` primary docs.
2. If needed, open the selected skill's doc map in its `references/` folder for full doc inventory.
3. If ambiguity remains, inspect the selected skill's source map in `references/` and listed source entry points.
4. Use targeted symbol search (`rg -n "<symbol_or_keyword>" src/gwaslab`) instead of broad source browsing.

## Skill Catalog
- `gwaslab-build-and-install`: Environment setup, install, bootstrap checks.
- `gwaslab-getting-started`: First analysis flow with `Sumstats`.
- `gwaslab-api-and-scripting`: API lifecycle and CLI/script interoperability.
- `gwaslab-inputs-and-modeling`: Input mapping and export-format planning.
- `gwaslab-simulation-workflows`: Standardization/harmonization and downstream runs.
- `gwaslab-analysis-and-output`: Visualization and reporting workflows.
- `gwaslab-examples-and-tutorials`: Reusable example and notebook-to-script routes.
- `gwaslab-troubleshooting`: Diagnostics and failure-mode handling.
- `gwaslab-advanced-topics`: Consolidated specialized/low-frequency docs.
- `gwaslab-parallel-hpc`: Compute scaling and batch execution guidance.

## Workspace Roots
- Docs: `docs/`
- Examples: `examples/`
- Tests: `test/`
- Source: `src/gwaslab/`
