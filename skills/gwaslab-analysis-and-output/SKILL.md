---
name: gwaslab-analysis-and-output
description: Use this skill for GWASLab visualization and reporting outputs, including mqq/regional/stacked/miami workflows, lead-variant annotations, and export/report patterns.
---

# gwaslab: Analysis and Output

## High-Signal Playbook
### Route Conditions
- Use this skill for plot generation, output tuning, and report-ready artifacts.
- Route to `gwaslab-getting-started` if data is not yet loadable/QCed.
- Route to `gwaslab-simulation-workflows` for harmonization or clumping prerequisites.
- Route to `gwaslab-inputs-and-modeling` for format-conversion-only requests.

### Triage Questions
- Which figure is required: `mqq`, `regional`, `stacked`, `miami`, correlation heatmap?
- Are input objects already QCed and build-tagged?
- Is region-specific LD annotation needed (VCF/recombination/GTF)?
- Are there one or two cohorts (for Miami/stacked comparisons)?
- Is the issue styling/parameter tuning or plotting failure?
- What final artifact is needed: figure only, lead table, or formatted output package?

### Canonical Workflow
1. Confirm input data quality and build before plotting (`docs/tutorial_v4.md`, `docs/visualization_mqq.md`).
2. Generate baseline `plot_mqq()` with `skip/cut` to control scale/performance (`docs/visualization_mqq.md`).
3. For locus detail, use `plot_mqq(mode="r", region=...)` with optional LD/gene tracks (`docs/visualization_regional.md`).
4. For comparisons, use `gl.plot_stacked_mqq()` or `gl.plot_miami2()` with `Sumstats` objects (`docs/visualization_stacked_mqq.md`, `docs/visualization_miami2.md`).
5. Extract/annotate lead variants with `get_lead()` and export with `to_format()` (`docs/utility_get_lead_novel.md`, `docs/Format.md`).
6. Cross-check known plotting edge cases in `KnownIssues` when outputs look inconsistent (`docs/KnownIssues.md`).

### Minimal Working Example
```python
import gwaslab as gl

s = gl.Sumstats("sumstats.tsv.gz", fmt="auto", build="19")
s.basic_check(verbose=False)

s.plot_mqq(skip=2, cut=20)
s.plot_mqq(mode="r", region=(7, 156538803, 157538803))
lead = s.get_lead(sig_level=5e-8)
s.to_format("analysis_ready", fmt="gwaslab")
```

### Pitfalls and Fixes
- `gl.plot_miami2()` called with file paths: pass `Sumstats` objects for `path1` and `path2` (`docs/visualization_miami2.md`).
- Regional plots missing LD context: provide reference VCF and matching build (`docs/visualization_regional.md`).
- Plotting full datasets is too slow/noisy: increase `skip` and use `cut`/`mode` adjustments (`docs/visualization_mqq.md`).
- Unexpected lead extraction in older versions: use updated package and check `KnownIssues` notes (`docs/KnownIssues.md`).
- Export formatting confusion after plotting: use explicit `to_format()` options and naming rules (`docs/Format.md`).

### Convergence and Validation Checks
- Figures render with expected panel/layout mode and no build mismatch warnings.
- Lead-variant counts are consistent with chosen significance/window settings.
- Annotation labels and highlighted loci map to expected SNPs/genes.
- Exported tables/files reopen cleanly and preserve plotted variant identifiers.

## Scope
- Visualization and output generation from QC-ready GWAS summary statistics.
- Includes parameter tuning and output packaging.

## Primary documentation references
- `docs/visualization_mqq.md`
- `docs/visualization_regional.md`
- `docs/visualization_stacked_mqq.md`
- `docs/visualization_miami2.md`
- `docs/visualization_plot_genetic_correlation.md`
- `docs/Format.md`
- `docs/format_load_save.md`
- `docs/KnownIssues.md`

## Workflow
- Start with docs examples for the requested plot mode.
- Use `references/doc_map.md` for wider option inventory.
- Escalate to source maps only when parameter behavior is unclear.

## Source entry points for unresolved issues
- `src/gwaslab/viz/viz_plot_mqqplot.py`
- `src/gwaslab/viz/viz_plot_regional2.py`
- `src/gwaslab/viz/viz_plot_stackedregional.py`
- `src/gwaslab/viz/viz_plot_stackedpanel.py`
- `src/gwaslab/viz/viz_plot_miamiplot2.py`
- `src/gwaslab/viz/viz_plot_rg_heatmap.py`
- `src/gwaslab/viz/viz_aux_quickfix.py`
- `src/gwaslab/viz/viz_aux_save_figure.py`
- `src/gwaslab/util/util_in_get_sig.py`
- `src/gwaslab/io/io_to_formats.py`
- Prefer targeted search: `rg -n "<symbol_or_keyword>" src/gwaslab/viz src/gwaslab/util src/gwaslab/io`
