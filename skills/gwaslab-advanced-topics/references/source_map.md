# gwaslab source map: Advanced Topics

Generated from source roots:
- `src`

Use this map only after exhausting the topic docs in `doc_map.md`.

## Topic query tokens
- `download_ref`
- `check_available_ref`
- `get_path`
- `vcf`
- `fasta`
- `gtf`
- `reserved_header`
- `infer_ancestry`
- `hapmap3`
- `get_lead`
- `get_novel`

## Fast source navigation
- `rg -n "<symbol_or_keyword>" src/gwaslab`
- `rg -n "^(def|class)\s+" src/gwaslab/bd/bd_download.py src/gwaslab/io/io_vcf.py src/gwaslab/io/io_fasta.py src/gwaslab/io/io_gtf.py`

## Suggested source entry points
- `src/gwaslab/bd/bd_download.py` | key functions: `check_available_ref`, `check_downloaded_ref`, `get_path`, `download_ref`
- `src/gwaslab/bd/bd_common_data.py` | key functions: `get_chr_to_NC`, `get_recombination_rate`, `get_chain`, `get_format_dict`
- `src/gwaslab/bd/bd_get_hapmap3.py` | key function: `_get_hapmap3`
- `src/gwaslab/io/io_vcf.py` | key functions: `is_vcf_file`, `check_vcf_chr_prefix`, `_get_ld_matrix_from_vcf`
- `src/gwaslab/io/io_fasta.py` | key functions: `parse_fasta`, `load_fasta_auto`, `load_fasta_filtered`, `get_fasta_record`
- `src/gwaslab/io/io_gtf.py` | key functions: `read_gtf`, `get_gtf`, `gtf_to_protein_coding`, `gtf_to_all_gene`
- `src/gwaslab/qc/qc_reserved_headers.py` | key functions: `get_default_sanity_ranges`, `_get_headers`, `_check_overlap_with_reserved_keys`
- `src/gwaslab/util/util_ex_infer_ancestry.py` | key functions: `_infer_ancestry`, `calculate_fst`
- `src/gwaslab/util/util_in_get_sig.py` | key functions: `_get_sig`, `_get_novel`, `_check_novel_set`
- `src/gwaslab/g_Sumstats.py` | key methods: `infer_ancestry`, `filter_hapmap3`, `get_lead`, `get_novel`

## Function-level behavior checks
- `pytest -q test/test_path_manager.py test/test_infer_build_and_hapmap3.py`
- `pytest -q test/test_read_fasta_chromosome_formats.py test/test_read_gtf_chromosome_formats.py`
- `pytest -q test/test_get_lead_top.py test/test_get_novel.py`
