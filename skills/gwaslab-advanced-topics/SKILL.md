---
name: gwaslab-advanced-topics
description: Use this skill for consolidated low-frequency GWASLab topics (reference-data management, VCF/FASTA/GTF IO, reserved headers, ancestry inference, update logs, and utility docs) that were merged to avoid one-doc routing fragmentation.
---

# gwaslab: Advanced Topics

## High-Signal Playbook
### Route Conditions
- Use this skill for specialized references/utilities not covered by core workflow skills.
- Route to `gwaslab-simulation-workflows` for end-to-end harmonization pipelines.
- Route to `gwaslab-inputs-and-modeling` for generic format/header mapping.

### Canonical Workflow
1. Open the exact topic doc first (`Download`, `Reference`, VCF/FASTA/GTF, `InferAncestry`, `reserved_header`).
2. Run the smallest reproducible check using local test/reference data.
3. Escalate to `references/source_map.md` only for implementation-level behavior.

### Minimal Checks
```python
import gwaslab as gl

print(gl.check_available_ref(show_all=False, verbose=False))
print(gl.get_path("1kg_eas_hg19"))
```

```bash
pytest -q test/test_read_fasta_chromosome_formats.py test/test_read_gtf_chromosome_formats.py
```

### Validation Checkpoints
- Reference key lookup returns a non-empty path or a clear missing-reference message.
- FASTA/GTF/VCF readers load expected chromosome naming styles.
- Reserved-header checks match expected column contracts.

## Scope
- Consolidated routing for specialized topics that each had narrow single-doc coverage.
- Keeps uncommon but important reference and utility content discoverable without fragmented routing.

## Route the request
- Reference asset catalogs/download paths/configuration -> `docs/Download.md`, `docs/Download_reference.md`, `docs/Reference.md`, `docs/CommonData.md`
- File-format internals (VCF/FASTA/GTF) -> `docs/VCF.md`, `docs/FASTA.md`, `docs/GTF.md`
- Data model/header contracts -> `docs/SumstatsObject.md`, `docs/reserved_header.md`
- Population and panel utilities -> `docs/InferAncestry.md`, `docs/Hapmap3.md`
- Lead/novel utility details -> `docs/utility_get_lead_novel.md`
- Release and method reference context -> `docs/UpdateLogs.md`, `docs/PaperReference.md`

## Workflow
- Start with the exact doc matching the specialized request.
- Use `references/doc_map.md` for full inventory and headings.
- Escalate to `references/source_map.md` only when behavior details are not explicit in docs.
- Cite exact documentation paths.

## Source entry points for unresolved issues
- `src/gwaslab/bd/bd_download.py`
- `src/gwaslab/bd/bd_common_data.py`
- `src/gwaslab/bd/bd_get_hapmap3.py`
- `src/gwaslab/io/io_vcf.py`
- `src/gwaslab/io/io_fasta.py`
- `src/gwaslab/io/io_gtf.py`
- `src/gwaslab/qc/qc_reserved_headers.py`
- `src/gwaslab/util/util_ex_infer_ancestry.py`
- `src/gwaslab/util/util_in_get_sig.py`
- `src/gwaslab/g_Sumstats.py`
- Prefer targeted search: `rg -n "<symbol_or_keyword>" src/gwaslab`
