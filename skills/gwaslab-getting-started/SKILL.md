---
name: gwaslab-getting-started
description: Use this skill for first GWASLab analyses after installation, including Sumstats loading, basic QC, first plots, lead-variant extraction, and first output export.
---

# gwaslab: Getting Started

## High-Signal Playbook
### Route Conditions
- Use this skill for first-run Python workflows and quick orientation around `gl.Sumstats`.
- Route to `gwaslab-build-and-install` if environment or CLI setup is not done.
- Route to `gwaslab-inputs-and-modeling` for detailed header mapping or format conversion matrices.
- Route to `gwaslab-simulation-workflows` for full harmonization and downstream pipelines.
- Route to `gwaslab-analysis-and-output` for advanced visualization tuning.

### Triage Questions
- What is the input file format (`auto` vs explicit columns)?
- Are genome build and allele conventions known?
- Does the user need API only, CLI only, or both?
- Is this a smoke test or production-scale run?
- Do they need lead variants, plots, or only cleaned output?
- Are reference files required in this first pass?

### Canonical Workflow
1. Import GWASLab and check version (`docs/index.md`, `docs/tutorial_v4.md`).
2. Load summary stats into `gl.Sumstats` with explicit columns or `fmt="auto"` (`docs/SumstatsObject.md`, `docs/tutorial_v4.md`).
3. Run `basic_check()` to standardize IDs/CHR/POS/alleles/stat columns (`docs/QC&Filtering.md`, `docs/tutorial_v4.md`).
4. Inspect `summary()` and `lookup_status()` for sanity and status-code interpretation (`docs/StatusCode.md`).
5. Run first analysis outputs: `plot_mqq()` and `get_lead()` (`docs/tutorial_v4.md`, `docs/Visualization.md`).
6. Save normalized output with `to_format()` (`docs/Format.md`, `docs/format_load_save.md`).

### Minimal Working Example
```python
import gwaslab as gl

s = gl.Sumstats(
    "sumstats.tsv.gz",
    fmt="auto",   # or explicit column names
    build="19"
)
s.basic_check(remove=True, remove_dup=True, verbose=False)
lead = s.get_lead(sig_level=5e-8)
s.plot_mqq(skip=2, cut=20)
s.to_format("first_pass", fmt="gwaslab")
```

### Pitfalls and Fixes
- `fmt="auto"` assumption is wrong for EA/EAF: switch to explicit column mapping (`README.md`, `docs/SumstatsObject.md`).
- CHR dtype or notation warnings after load: run `fix_chr()`/`basic_check()` and re-check (`docs/tutorial_v4.md`).
- Unknown build (`99`) causes downstream ambiguity: set/infer build before harmonization or regional plotting (`docs/InferBuild.md`).
- Slow initial runs on large files: use `nrows`, `chrom_pat`, or toy/sample data first (`docs/format_load_save.md`).
- Empty lead set after filtering: verify significance threshold/window and input `P`/`MLOG10P` integrity (`docs/utility_get_lead_novel.md`, `docs/KnownIssues.md`).

### Convergence and Validation Checks
- Post-QC dataframe has canonical core headers (`SNPID, CHR, POS, EA, NEA, STATUS, ...`).
- `lookup_status()` output is interpretable and consistent with performed steps.
- `plot_mqq()` renders without coordinate/format errors.
- `get_lead()` returns stable lead count under expected `sig_level` and window.
- `to_format()` writes expected file and log artifacts.

## Scope
- First-day usage: load, QC, quick analysis, and export.
- Docs-first guidance with minimal source escalation.

## Primary documentation references
- `docs/index.md`
- `docs/tutorial_v4.md`
- `docs/SumstatsObject.md`
- `docs/QC&Filtering.md`
- `docs/StatusCode.md`
- `docs/Visualization.md`
- `docs/Format.md`
- `docs/format_load_save.md`

## Workflow
- Start with primary docs.
- If details are missing, inspect `references/doc_map.md`.
- Escalate to `references/source_map.md` only after docs are exhausted.
- Cite exact doc paths.

## Source entry points for unresolved issues
- `src/gwaslab/g_Sumstats.py`
- `src/gwaslab/io/io_preformat_input.py`
- `src/gwaslab/qc/qc_fix_sumstats.py`
- `src/gwaslab/qc/qc_sanity_check.py`
- `src/gwaslab/util/util_in_get_sig.py`
- `src/gwaslab/viz/viz_plot_mqqplot.py`
- `src/gwaslab/view/view_report.py`
- Prefer targeted search: `rg -n "<symbol_or_keyword>" src/gwaslab`
