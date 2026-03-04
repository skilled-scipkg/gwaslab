---
name: gwaslab-simulation-workflows
description: Use this skill for GWASLab QC-standardization, harmonization, clumping, and downstream pipeline execution (CLI/API), including LDSC-oriented run paths.
---

# gwaslab: Simulation Workflows

## High-Signal Playbook
### Route Conditions
- Use this skill for end-to-end processing pipelines: standardization, harmonization, lead/clump extraction, and downstream analysis handoff.
- Route to `gwaslab-inputs-and-modeling` for pure format/header conversion tasks.
- Route to `gwaslab-analysis-and-output` for plotting/reporting decisions.
- Route to `gwaslab-troubleshooting` for failure-driven diagnosis and edge cases.

### Triage Questions
- Is the current file already QCed (`basic_check`) or raw?
- Which genome build is used, and is liftover needed?
- Which references are available (`ref_seq`, `ref_infer`, `ref_rsid_vcf/tsv`)?
- Is this a high-throughput run that needs `sweep_mode`/threads?
- Is output for clumping, LDSC, or meta-analysis prep?
- Should bad/duplicate variants be removed during QC?

### Canonical Workflow
1. Load data and run `basic_check(remove=..., remove_dup=...)` (`docs/standardization_workflow.md`, `docs/CLIWorkflowExamples.md`).
2. Harmonize with references (`harmonize(...)`) and tuned MAF settings (`docs/harmonization_workflow.md`, `docs/Harmonization.md`).
3. Inspect harmonization/QC status (`summary()`, `lookup_status()`) (`docs/tutorial_v4.md`).
4. Extract lead variants or clump with PLINK-backed utilities (`docs/utility_get_lead_novel.md`, `docs/util_ex_clumping.md`).
5. Prepare downstream outputs (for LDSC/meta) via `to_format()` or CLI (`docs/CLI.md`, `docs/ldsc_in_gwaslab.md`).
6. If liftover is applied, reharmonize before downstream steps (`docs/tutorial_v4.md`, `docs/LiftOver.md`).

### Minimal Working Example
```python
import gwaslab as gl

s = gl.Sumstats("sumstats.tsv.gz", fmt="auto", build="19")
s.basic_check(remove=True, remove_dup=True, verbose=False)
s.harmonize(
    basic_check=False,
    ref_seq=gl.get_path("ucsc_genome_hg19"),
    ref_rsid_vcf=gl.get_path("dbsnp_v151_hg19"),
    ref_infer=gl.get_path("1kg_eas_hg19"),
    ref_alt_freq="AF",
    sweep_mode=True,
    threads=4,
    verbose=False,
)
lead = s.get_lead(sig_level=5e-8)
s.to_format("harmonized", fmt="gwaslab")
```

### Pitfalls and Fixes
- Running harmonization without matching build/reference: infer/set build and align reference assets first (`docs/Harmonization.md`).
- Not providing `ref_alt_freq` for strand inference on custom VCF: set the correct INFO AF field (`docs/harmonization_workflow.md`).
- Large datasets time out in lookup mode: switch to `sweep_mode=True` and raise threads (`docs/CLI.md`).
- Clumping fails due missing PLINK2 or reference LD files: validate executable/path and VCF assets (`docs/util_ex_clumping.md`).
- Liftover applied without re-harmonization: rerun harmonization before final outputs (`docs/tutorial_v4.md`).

### Convergence and Validation Checks
- QC/harmonization summary shows expected step completion and nonzero processed variants.
- Harmonization reports acceptable flip/match rates and expected unresolved counts.
- Lead/clump outputs are stable under reasonable window/threshold settings.
- LDSC or downstream export files are format-valid and loadable by target tools.

## Scope
- Standard GWAS processing pipelines in GWASLab from raw to harmonized outputs.
- Includes API and CLI run paths when workflow control is the primary task.

## Primary documentation references
- `docs/standardization_workflow.md`
- `docs/harmonization_workflow.md`
- `docs/Harmonization.md`
- `docs/CLIWorkflowExamples.md`
- `docs/util_ex_clumping.md`
- `docs/utility_data_conversion.md`
- `docs/ldsc_in_gwaslab.md`
- `docs/MetaAnalysis.md`

## Workflow
- Start with docs and examples.
- Use `references/doc_map.md` for full topic coverage.
- Use `references/source_map.md` only when behavior remains ambiguous.

## Source entry points for unresolved issues
- `src/gwaslab/g_Sumstats.py`
- `src/gwaslab/qc/qc_fix_sumstats.py`
- `src/gwaslab/qc/qc_sanity_check.py`
- `src/gwaslab/hm/hm_harmonize_sumstats.py`
- `src/gwaslab/hm/hm_assign_rsid.py`
- `src/gwaslab/hm/hm_infer_with_af.py`
- `src/gwaslab/util/util_ex_run_clumping.py`
- `src/gwaslab/util/util_ex_ldsc.py`
- `src/gwaslab/CLI/cli.py`
- Prefer targeted search: `rg -n "<symbol_or_keyword>" src/gwaslab`
