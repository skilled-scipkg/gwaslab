---
name: gwaslab-inputs-and-modeling
description: Use this skill for GWAS summary-statistics ingestion, header/format modeling, CLI/API input mapping, and export-format planning in GWASLab.
---

# gwaslab: Inputs and Modeling

## High-Signal Playbook
### Route Conditions
- Use this skill for input schema mapping, loading strategy, and output format conversion.
- Route to `gwaslab-build-and-install` for environment/bootstrap issues.
- Route to `gwaslab-simulation-workflows` for harmonization/QC pipelines beyond format setup.
- Route to `gwaslab-analysis-and-output` for plotting-focused tasks.

### Triage Questions
- Is input a file path, dataframe, or chromosome-sharded files (`@` pattern)?
- Which columns are available for SNP identifiers and alleles?
- Should `fmt="auto"` be trusted, or are explicit mappings needed?
- What output target is required (`gwaslab`, `ldsc`, `plink`, `vcf`, `ssf`, etc.)?
- Are HLA/HapMap3 filters required at export time?
- Does the user need CLI reproducibility or Python-only flow?

### Canonical Workflow
1. Select ingestion mode: explicit columns, known format, or `auto` (`docs/SumstatsObject.md`, `docs/format_load_save.md`).
2. Use targeted loading for large files (`nrows`, `chrom_pat`, `snpid_pat`) to validate schema quickly (`docs/format_load_save.md`).
3. Run `basic_check()` and selective `fill_data()` to build required statistical columns (`docs/format_load_save.md`, `docs/utility_data_conversion.md`).
4. Validate required headers for downstream target formats (`docs/reserved_header.md`, `docs/Format.md`).
5. Export with `to_format()`/CLI and required filters (`hapmap3`, `exclude_hla`, compression/indexing) (`docs/Format.md`, `docs/CLI.md`).

### Minimal Working Example
```python
import gwaslab as gl

s = gl.Sumstats("sumstats.tsv.gz", fmt="auto", build="19", nrows=500000)
s.basic_check(verbose=False)
s.fill_data(to_fill=["Z", "MLOG10P"], verbose=False)
s.to_format("ready_for_ldsc", fmt="ldsc", hapmap3=True, exclude_hla=True)
```

```bash
gwaslab --input sumstats.tsv.gz --fmt auto --qc --out cleaned --to-fmt gwaslab
gwaslab --input cleaned.gwaslab.tsv.gz --fmt gwaslab --out ldsc_ready --to-fmt ldsc --hapmap3 --exclude-hla
```

### Pitfalls and Fixes
- Auto mode header assumptions do not match study conventions: use explicit column args (`docs/SumstatsObject.md`).
- Missing derived stats for downstream tools: call `fill_data()` for `Z`, `MLOG10P`, etc. (`docs/utility_data_conversion.md`).
- CHR notation mismatch (`chr1` vs `1`): normalize before export (`docs/format_load_save.md`).
- `tabix` requested without compatible bgzip mode: use format-specific settings (`docs/Format.md`).
- Unexpected output names: follow CLI/`to_format()` naming conventions (`docs/CLI.md`, `docs/Format.md`).

### Convergence and Validation Checks
- Core reserved headers and dtypes are valid for target export.
- Export file exists with expected suffix and columns.
- Optional filters (HapMap3/HLA) reduce variants as expected.
- Round-trip load of exported file works for the chosen format.

## Scope
- Input schema decisions and output format modeling.
- API/CLI interoperability for reproducible data-flow setup.

## Primary documentation references
- `docs/SumstatsObject.md`
- `docs/format_load_save.md`
- `docs/CLI.md`
- `docs/Format.md`
- `docs/utility_data_conversion.md`
- `docs/reserved_header.md`

## Workflow
- Use docs first.
- Use `references/doc_map.md` for complete inventory.
- Escalate to `references/source_map.md` when behavior details are unresolved.

## Source entry points for unresolved issues
- `src/gwaslab/io/io_preformat_input.py`
- `src/gwaslab/io/io_input_type.py`
- `src/gwaslab/io/io_to_formats.py`
- `src/gwaslab/io/io_gwaslab_standard.py`
- `src/gwaslab/util/util_in_fill_data.py`
- `src/gwaslab/bd/bd_sumstats_formats.py`
- `src/gwaslab/CLI/cli.py`
- `src/gwaslab/g_Sumstats.py`
- Prefer targeted search: `rg -n "<symbol_or_keyword>" src/gwaslab`
