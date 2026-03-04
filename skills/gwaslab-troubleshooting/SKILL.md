---
name: gwaslab-troubleshooting
description: Use this skill for diagnosing GWASLab failures or unexpected outputs across loading, QC, harmonization, plotting, and export; prioritize reproducible checks and targeted fixes.
---

# gwaslab: Troubleshooting

## High-Signal Playbook
### Route Conditions
- Use this skill when the user reports an error, mismatch, empty output, or suspicious behavior.
- Route to a topic skill only after the failure mode is isolated.

### Triage Checklist
- Capture exact command/API call and full traceback/log excerpt.
- Confirm input schema (`fmt`, required columns, build, allele columns).
- Confirm reference assets exist and match build.
- Reproduce with a minimal dataset (`test/raw/dirty_sumstats.tsv` or `--nrows`).
- Determine whether behavior is expected (KnownIssues/StatusCode) or regression.

### Canonical Workflow
1. Re-run minimal reproducible command with explicit options and `--threads 1`.
2. Check status and QC summaries (`lookup_status()`, sanity checks).
3. Isolate stage: load, QC, harmonize, clump, plot, export.
4. Open stage-specific docs and `references/source_map.md` for function-level inspection.
5. Validate fix with focused tests before broad reruns.

### Minimal Repro Commands
```bash
gwaslab --input test/raw/dirty_sumstats.tsv --fmt gwaslab --qc --remove --remove-dup --out triage_qc --to-fmt gwaslab --threads 1
pytest -q test/test_sumstats_object.py test/test_qc_and_harmonize.py
```

```python
import gwaslab as gl
s = gl.Sumstats("test/raw/dirty_sumstats.tsv", fmt="gwaslab")
s.basic_check(remove=True, remove_dup=True, verbose=False)
print(s.lookup_status())
```

### Validation Checkpoints
- Failure is reproducible with a minimal command/input.
- Suspected fix changes only the failing stage behavior.
- Focused tests for that stage pass before full workflow rerun.

## Scope
- Known issues, diagnostics, and failure isolation across GWASLab workflows.
- Practical debugging steps for both API and CLI paths.

## Primary documentation references
- `docs/KnownIssues.md`
- `docs/StatusCode.md`
- `docs/QC&Filtering.md`
- `docs/Harmonization.md`
- `docs/CLI.md`
- `docs/reserved_header.md`
- `test/common_cases.txt`

## Workflow
- Start with known-issue/status docs and a minimal reproducible run.
- Use `references/doc_map.md` for additional diagnostics docs.
- Escalate to `references/source_map.md` for code-level behavior checks.

## Source entry points for unresolved issues
- `src/gwaslab/CLI/cli.py`
- `src/gwaslab/g_Sumstats.py`
- `src/gwaslab/io/io_preformat_input.py`
- `src/gwaslab/qc/qc_fix_sumstats.py`
- `src/gwaslab/qc/qc_sanity_check.py`
- `src/gwaslab/qc/qc_reserved_headers.py`
- `src/gwaslab/hm/hm_harmonize_sumstats.py`
- `src/gwaslab/util/util_in_fill_data.py`
- `src/gwaslab/util/util_in_get_sig.py`
- `src/gwaslab/viz/viz_plot_mqqplot.py`
- Prefer targeted source search: `rg -n "<symbol_or_keyword>" src/gwaslab`
