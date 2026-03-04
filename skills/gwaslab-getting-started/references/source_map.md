# gwaslab source map: Getting Started

Generated from source roots:
- `src`

Use this map only after exhausting the topic docs in `doc_map.md`.

## Topic query tokens
- `sumstats`
- `basic_check`
- `lookup_status`
- `plot_mqq`
- `get_lead`
- `to_format`
- `report`

## Fast source navigation
- `rg -n "<symbol_or_keyword>" src/gwaslab`
- `rg -n "^\s+def\s+(basic_check|lookup_status|plot_mqq|get_lead|to_format)" src/gwaslab/g_Sumstats.py`

## Suggested source entry points
- `src/gwaslab/g_Sumstats.py` | key methods: `basic_check`, `lookup_status`, `plot_mqq`, `get_lead`, `to_format`
- `src/gwaslab/io/io_preformat_input.py` | key function: `_preformat` for first-load parsing
- `src/gwaslab/qc/qc_fix_sumstats.py` | key functions: `_fix_ID`, `_fix_chr`, `_fix_pos`, `_fix_allele`, `_remove_dup`
- `src/gwaslab/qc/qc_sanity_check.py` | key functions: `_sanity_check_stats`, `_check_data_consistency`
- `src/gwaslab/util/util_in_get_sig.py` | key functions: `_get_sig`, `_get_top`
- `src/gwaslab/viz/viz_plot_mqqplot.py` | key function: `_mqqplot`
- `src/gwaslab/io/io_to_formats.py` | key functions: `_to_format`, `_write_tabular`
- `src/gwaslab/view/view_report.py` | key function: `generate_qc_report`

## Function-level behavior checks
- `pytest -q test/test_sumstats_object.py test/test_sumstats_chaining.py`
- `pytest -q test/test_qc_and_harmonize.py test/test_get_lead_top.py`
- `pytest -q test/test_viz_mqqplot.py test/test_report.py`
