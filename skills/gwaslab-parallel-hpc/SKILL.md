---
name: gwaslab-parallel-hpc
description: Use this skill for GWASLab performance scaling on multi-core systems (threaded QC/harmonization and external-tool wrappers), including batch/cluster execution patterns.
---

# gwaslab: Parallel and HPC

## High-Signal Playbook
### Route Conditions
- Use this skill for runtime/performance scaling, multi-core tuning, and batch scheduling strategy.
- Route to `gwaslab-build-and-install` for environment/toolchain setup.
- Route to `gwaslab-simulation-workflows` for full biological pipeline logic.

### Triage Questions
- Which stage is slow: load, QC, harmonization, clumping, LDSC, plotting, or export?
- Is the run API-based or CLI-based?
- What CPU threads, RAM limits, and storage bandwidth are available?
- Are external binaries available (`plink2`, `ldsc`), and where are they on PATH?
- Is the workload one large file or many traits/chunks?

### Canonical Workflow
1. Start with a small subset (`--nrows`) and baseline single-thread timings.
2. Scale thread-sensitive operations only (`--threads`, `sweep_mode=True`) and remeasure.
3. For external tools (PLINK/LDSC), verify binary invocation and IO paths first.
4. For cluster/batch use, split by trait/chromosome and aggregate outputs afterward.

### Minimal Commands
```bash
# Baseline
/usr/bin/time -v gwaslab --input test/raw/to_harmonize.tsv --fmt gwaslab --qc --out baseline --to-fmt gwaslab --threads 1

# Scaled harmonization-style run
/usr/bin/time -v gwaslab --input test/raw/to_harmonize.tsv --fmt gwaslab --qc --harmonize --ref-seq test/ref/chr7.fasta.gz --ref-rsid-vcf test/ref/b157_2564.vcf.gz --ref-infer test/ref/1kg_eas_hg19.chr7_126253550_128253550.vcf.gz --sweep-mode --threads 4 --out scaled --to-fmt gwaslab
```

### Validation Checkpoints
- Multi-thread run is functionally identical to 1-thread for core output columns/counts.
- Throughput improvement is measurable without unacceptable memory spikes.
- External wrappers fail fast with clear errors when binaries/refs are missing.

## Scope
- Threaded and external-tool performance scaling in GWASLab.
- Practical CPU/batch execution patterns for simulation-oriented workloads.

## Primary documentation references
- `docs/CLI.md`
- `docs/CLIWorkflowExamples.md`
- `docs/harmonization_workflow.md`
- `docs/util_ex_clumping.md`
- `docs/ldsc_in_gwaslab.md`
- `docs/LoadLDSC.md`

## Workflow
- Start with docs for the target stage.
- Use `references/doc_map.md` for broader coverage.
- Escalate to `references/source_map.md` for thread/external-wrapper internals.

## Source entry points for unresolved issues
- `src/gwaslab/CLI/cli.py`
- `src/gwaslab/g_Sumstats.py`
- `src/gwaslab/hm/hm_harmonize_sumstats.py`
- `src/gwaslab/hm/hm_assign_rsid.py`
- `src/gwaslab/qc/qc_fix_sumstats.py`
- `src/gwaslab/util/util_ex_run_clumping.py`
- `src/gwaslab/util/util_ex_ldsc.py`
- `src/gwaslab/util/cwrapper/util_ex_command_runner.py`
- `src/gwaslab/util/rwrapper/util_ex_r_runner.py`
- `src/gwaslab/util/pwrapper/util_ex_python_runner.py`
- Prefer targeted source search: `rg -n "<symbol_or_keyword>" src/gwaslab`
