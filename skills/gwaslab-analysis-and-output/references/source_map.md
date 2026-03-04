# gwaslab source map: Analysis and Output

Generated from source roots:
- `src`

Use this map only after exhausting the topic docs in `doc_map.md`.

## Topic query tokens
- `plot_mqq`
- `plot_region`
- `plot_stacked_mqq`
- `plot_miami2`
- `plot_rg`
- `compare_effect`
- `get_lead`
- `get_novel`
- `to_format`

## Fast source navigation
- `rg -n "<symbol_or_keyword>" src/gwaslab/viz src/gwaslab/util src/gwaslab/io`
- `rg -n "^\s+def\s+(plot_mqq|plot_region|get_lead|get_novel|to_format)" src/gwaslab/g_Sumstats.py`

## Suggested source entry points
- `src/gwaslab/g_Sumstats.py` | key methods: `plot_mqq`, `plot_region`, `get_lead`, `get_novel`, `to_format`
- `src/gwaslab/viz/viz_plot_mqqplot.py` | key function: `_mqqplot`
- `src/gwaslab/viz/viz_plot_regional2.py` | key functions: `_plot_regional`, `process_vcf`, `process_ld`, `process_gtf`
- `src/gwaslab/viz/viz_plot_stackedregional.py` | key function: `plot_stacked_mqq`
- `src/gwaslab/viz/viz_plot_miamiplot2.py` | key function: `plot_miami2`
- `src/gwaslab/viz/viz_plot_rg_heatmap.py` | key function: `plot_rg`
- `src/gwaslab/viz/viz_plot_compare_effect.py` | key function: `compare_effect`
- `src/gwaslab/viz/viz_aux_save_figure.py` | key functions: `save_figure`, `get_default_path`
- `src/gwaslab/util/util_in_get_sig.py` | key functions: `_get_sig`, `_get_novel`, `_anno_gene`
- `src/gwaslab/io/io_to_formats.py` | key functions: `_to_format`, `_write_tabular`
- `src/gwaslab/view/view_report.py` | key function: `generate_qc_report`

## Function-level behavior checks
- `pytest -q test/test_viz_mqqplot.py test/test_viz_related_plots.py test/test_viz_panel.py`
- `pytest -q test/test_get_lead_top.py test/test_get_novel.py`
- `pytest -q test/test_read_ldsc_plot_rg.py test/test_viz_compare_effect.py`
- `pytest -q test/test_io_to_formats.py test/test_report.py`
