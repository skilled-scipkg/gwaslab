---
name: gwaslab-api-and-scripting
description: Use this skill for GWASLab Sumstats API lifecycle questions, command-line automation, and Python/CLI interoperability in scripted pipelines.
---

# gwaslab: API and Scripting

## High-Signal Playbook
### Route Conditions
- Use this skill for API/CLI method mapping, batch automation, and script reproducibility.
- Route to `gwaslab-getting-started` for first-run basics.
- Route to `gwaslab-inputs-and-modeling` for schema and export-only questions.
- Route to `gwaslab-simulation-workflows` for harmonization/clumping/downstream pipeline design.

### Canonical Workflow
1. Load with `gl.Sumstats(...)` and run `basic_check()` when needed (`docs/SumstatsObject.md`, `docs/CLI.md`).
2. Apply analysis/action methods (`harmonize`, `get_lead`, `to_format`) in deterministic order.
3. Convert the same flow to CLI for batch reproducibility (`docs/CLIWorkflowExamples.md`).
4. Validate API/CLI parity on a small subset before full runs.

### Minimal API/CLI Parity Check
```python
import gwaslab as gl

s = gl.Sumstats("test/raw/dirty_sumstats.tsv", fmt="gwaslab")
s.basic_check(remove=True, remove_dup=True, verbose=False)
out = s.get_lead(sig_level=5e-8)
print(len(s.data), len(out))
```

```bash
gwaslab --input test/raw/dirty_sumstats.tsv --fmt gwaslab --qc --remove --remove-dup --out tmp_api_cli_check --to-fmt gwaslab
```

### Validation Checkpoints
- API and CLI both complete without parser/runtime errors.
- Expected core columns remain after `basic_check()`.
- Output file from CLI exists and reloads via `gl.Sumstats(..., fmt="gwaslab")`.

## Scope
- Programmatic `gl.Sumstats` lifecycle: load, QC/harmonize, analysis methods, and output.
- CLI command construction and translation between API and CLI workflows.
- Script-level reproducibility and batch processing patterns.

## Primary documentation references
- `docs/SumstatsObject.md`
- `docs/CLI.md`
- `docs/CLIWorkflowExamples.md`
- `docs/format_load_save.md`
- `docs/tutorial_v4.md`

## Workflow
- Start with docs above and map requested operation to API or CLI primitive.
- Prefer API for in-memory chaining/custom logic; prefer CLI for reproducible batch jobs.
- Use examples in `docs/CLIWorkflowExamples.md` for multi-step scripting templates.
- If docs are insufficient, inspect `references/doc_map.md`, then `references/source_map.md`.
- Cite exact doc paths.

## API lifecycle anchors
- `gl.Sumstats(...)` -> load/normalize input schema.
- `basic_check(...)` / `harmonize(...)` -> core data-processing stages.
- `get_lead(...)`, `plot_mqq(...)`, `clump(...)` -> analysis utilities.
- `to_format(...)` / `to_pickle(...)` -> persistence and interchange.

## Source entry points for unresolved issues
- `src/gwaslab/g_Sumstats.py`
- `src/gwaslab/CLI/cli.py`
- `src/gwaslab/__init__.py`
- `src/gwaslab/io/io_preformat_input.py`
- `src/gwaslab/io/io_to_formats.py`
- `src/gwaslab/hm/hm_harmonize_sumstats.py`
- `src/gwaslab/util/util_in_fill_data.py`
- Prefer targeted search: `rg -n "<symbol_or_keyword>" src/gwaslab`
