---
name: gwaslab-build-and-install
description: Use this skill for GWASLab environment setup, package installation, CLI/Python smoke tests, and first-time reference-data bootstrap; escalate to source only when docs do not explain behavior.
---

# gwaslab: Build and Install

## High-Signal Playbook
### Route Conditions
- Use this skill for environment setup, install/upgrade, CLI bootstrap, and first-run dependency checks.
- Route to `gwaslab-getting-started` after install is complete and the user asks for first analysis steps.
- Route to `gwaslab-inputs-and-modeling` for file-format mapping and output conversion details.
- Route to `gwaslab-simulation-workflows` for QC/harmonization pipelines and downstream runs.

### Triage Questions
- Which Python version is available (prefer 3.12)?
- Will the user run Python API, CLI, or both?
- Is this a clean environment or an existing one?
- Do they need reference data now (FASTA/VCF/dbSNP/1KG)?
- What genome build will they process first (19/38)?
- Is a quick smoke test enough, or do they want a full first pass?

### Canonical Workflow
1. Create/activate a Python 3.12 environment and install GWASLab (`README.md`, `docs/index.md`).
2. Verify install with `gwaslab version` and `import gwaslab as gl; gl.show_version()` (`docs/index.md`).
3. Run a smoke load on a small file (`--nrows` or small sample) to validate IO and dtype checks (`docs/CLI.md`, `docs/tutorial_v4.md`).
4. Confirm CLI path and core flags (`--qc`, `--harmonize`, `--to-fmt`) (`docs/CLI.md`).
5. If harmonization is planned, verify/download reference assets (`gl.check_available_ref()`, `gl.download_ref()`) (`docs/Download.md`, `docs/Download_reference.md`).
6. If genome build is uncertain, run `infer_build` before large jobs (`docs/InferBuild.md`).

### Minimal Working Example
```bash
conda create -n gwaslab -c conda-forge python=3.12 -y
conda activate gwaslab
pip install -U gwaslab

gwaslab version
gwaslab --input sumstats.tsv --fmt auto --nrows 1000 --qc --out smoke --to-fmt gwaslab
```

```python
import gwaslab as gl
gl.show_version()
print(gl.check_available_ref(show_all=False, verbose=False))
```

### Pitfalls and Fixes
- `fmt=auto` misinterprets alleles/frequency assumptions: switch to explicit column mapping (`README.md`, `docs/SumstatsObject.md`).
- Install works but CLI missing: confirm environment activation and `python -m gwaslab` fallback (`src/gwaslab/__main__.py`).
- Harmonization fails due missing references: download required FASTA/VCF/index files first (`docs/Download_reference.md`).
- Build mismatch creates downstream confusion: run `infer_build()` and set build before harmonization/liftover (`docs/InferBuild.md`, `docs/LiftOver.md`).
- Large dbSNP downloads stall: start with smaller processed references for workflow validation (`docs/Download.md`).

### Convergence and Validation Checks
- `gl.show_version()` and `gwaslab version` both return expected version string.
- Smoke CLI run writes output and log files with expected naming (`docs/CLI.md`).
- Loaded data shows canonical columns after QC reordering (`docs/tutorial_v4.md`).
- Reference lookup path resolves for required key(s) before harmonization.

## Scope
- Build, installation, environment setup, and first-run validation.
- Keep responses operational and docs-first.

## Primary documentation references
- `README.md`
- `docs/index.md`
- `docs/CLI.md`
- `docs/tutorial_v4.md`
- `docs/Download.md`
- `docs/Download_reference.md`
- `docs/InferBuild.md`
- `docs/LiftOver.md`

## Workflow
- Start with the primary references above.
- If details are missing, inspect `references/doc_map.md`.
- Only then inspect `references/source_map.md` and targeted files below.
- Cite exact documentation file paths in responses.

## Source entry points for unresolved issues
- `src/gwaslab/CLI/cli.py`
- `src/gwaslab/__main__.py`
- `src/gwaslab/__init__.py`
- `src/gwaslab/g_Sumstats.py`
- `src/gwaslab/io/io_preformat_input.py`
- `src/gwaslab/bd/bd_download.py`
- `src/gwaslab/qc/qc_build.py`
- `src/gwaslab/hm/hm_liftover_v2.py`
- Prefer targeted search: `rg -n "<symbol_or_keyword>" src/gwaslab`
