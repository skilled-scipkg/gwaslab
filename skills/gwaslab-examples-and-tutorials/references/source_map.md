# gwaslab source map: Examples and Tutorials

Generated from source roots:
- `src`

Use this map only after exhausting the topic docs in `doc_map.md`.

## Topic query tokens
- `tutorial`
- `workflow`
- `basic_check`
- `harmonize`
- `get_lead`
- `to_format`
- `plot_mqq`
- `plot_region`
- `clump`

## Fast source navigation
- `rg -n "<symbol_or_keyword>" src/gwaslab`
- `rg -n "^\s+def\s+(basic_check|harmonize|get_lead|plot_mqq|to_format|clump)" src/gwaslab/g_Sumstats.py`

## Suggested source entry points
- `src/gwaslab/g_Sumstats.py` | notebook-to-script core methods (`basic_check`, `harmonize`, `get_lead`, `plot_mqq`, `to_format`, `clump`)
- `src/gwaslab/CLI/cli.py` | CLI equivalents for tutorial pipelines
- `src/gwaslab/io/io_preformat_input.py` | first-cell load behavior and column mapping
- `src/gwaslab/util/util_in_fill_data.py` | conversion helpers commonly used in examples
- `src/gwaslab/util/util_in_get_sig.py` | lead/novel extraction logic
- `src/gwaslab/util/util_ex_run_clumping.py` | clumping wrapper for external-tool notebooks
- `src/gwaslab/util/util_ex_ldsc.py` | LDSC wrapper used in external utility examples
- `src/gwaslab/viz/viz_plot_mqqplot.py` | MQQ figure behavior
- `src/gwaslab/viz/viz_plot_regional2.py` | regional figure behavior
- `src/gwaslab/viz/viz_plot_stackedregional.py` | stacked/Miami-style comparison figures

## Function-level behavior checks
- `pytest -q test/test_tutorial_v4.py test/test_sumstats_chaining.py`
- `pytest -q test/test_get_lead_top.py test/test_qc_and_harmonize.py`
- `pytest -q test/test_viz_mqqplot.py test/test_viz_related_plots.py`
- `pytest -q test/test_clumping.py test/test_ldsc.py`
