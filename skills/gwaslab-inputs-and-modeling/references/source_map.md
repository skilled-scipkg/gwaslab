# gwaslab source map: Inputs and Modeling

Generated from source roots:
- `src`

Use this map only after exhausting the topic docs in `doc_map.md`.

## Topic query tokens
- `preformat`
- `detect_sumstats_format`
- `fill_data`
- `to_format`
- `gsf`
- `reserved_headers`
- `cli`

## Fast source navigation
- `rg -n "<symbol_or_keyword>" src/gwaslab`
- `rg -n "^(def|class)\s+" src/gwaslab/io/io_preformat_input.py src/gwaslab/io/io_to_formats.py src/gwaslab/io/io_gwaslab_standard.py`

## Suggested source entry points
- `src/gwaslab/io/io_preformat_input.py` | key functions: `_preformat`, `_build_column_mappings`, `_load_sumstats_data`
- `src/gwaslab/io/io_input_type.py` | key function: `_get_id_column`
- `src/gwaslab/bd/bd_sumstats_formats.py` | key functions: `detect_sumstats_format`, `read_header_and_rows`
- `src/gwaslab/io/io_to_formats.py` | key functions: `_to_format`, `tofmt`, `_write_tabular`
- `src/gwaslab/io/io_gwaslab_standard.py` | key functions: `write_gsf`, `load_gsf`
- `src/gwaslab/util/util_in_fill_data.py` | key functions: `_fill_data`, `fill_iteratively`, `fill_mlog10p`
- `src/gwaslab/qc/qc_reserved_headers.py` | key functions: `_get_headers`, `get_default_sanity_ranges`
- `src/gwaslab/CLI/cli.py` | key function: `_process_sumstats` for CLI-to-format pipeline

## Function-level behavior checks
- `pytest -q test/test_preformat_input.py test/test_io_to_formats.py`
- `pytest -q test/test_gsf_io.py test/test_validate_ssf.py`
- `pytest -q test/test_fill_data.py`
