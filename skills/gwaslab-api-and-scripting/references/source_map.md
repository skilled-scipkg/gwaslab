# gwaslab source map: API and Scripting

Generated from source roots:
- `src`

Use this map only after exhausting the topic docs in `doc_map.md`.

## Topic query tokens
- `sumstats`
- `cli`
- `basic_check`
- `harmonize`
- `assign_rsid`
- `rsid_to_chrpos`
- `fill_data`
- `to_format`
- `pipeline`

## Fast source navigation
- `rg -n "<symbol_or_keyword>" src/gwaslab`
- `rg -n "^\s+def\s+(basic_check|harmonize|assign_rsid|rsid_to_chrpos|fill_data|to_format)" src/gwaslab/g_Sumstats.py`
- `rg -n "^(def|class)\s+" src/gwaslab/CLI/cli.py src/gwaslab/io/io_preformat_input.py src/gwaslab/io/io_to_formats.py`

## Suggested source entry points
- `src/gwaslab/g_Sumstats.py` | key methods: `basic_check`, `harmonize`, `assign_rsid`, `rsid_to_chrpos`, `fill_data`, `to_format`
- `src/gwaslab/CLI/cli.py` | key functions: `_process_sumstats`, `main`; CLI argument-to-method mapping
- `src/gwaslab/io/io_preformat_input.py` | key functions: `_preformat`, `_load_sumstats_data`, `_build_column_mappings`
- `src/gwaslab/io/io_to_formats.py` | key functions: `_to_format`, `tofmt`, `_write_tabular`, `_process_vcf_header`
- `src/gwaslab/hm/hm_harmonize_sumstats.py` | key functions: `assign_rsid_single`, `check_status`, `checkaf`
- `src/gwaslab/hm/hm_assign_rsid.py` | key functions: `_assign_rsid`, `_annotate_sumstats`, `_assign_from_lookup`
- `src/gwaslab/util/util_in_fill_data.py` | key functions: `_fill_data`, `fill_iteratively`, `fill_p`, `fill_z`
- `src/gwaslab/util/util_in_get_sig.py` | key functions: `_get_sig`, `_get_top`

## Function-level behavior checks
- `pytest -q test/test_cli.py test/test_sumstats_object.py`
- `pytest -q test/test_preformat_input.py test/test_io_to_formats.py`
- `pytest -q test/test_qc_and_harmonize.py test/test_rsid_to_chrpos_hdf5.py`
