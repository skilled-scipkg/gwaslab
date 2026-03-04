# gwaslab source map: Troubleshooting

Generated from source roots:
- `src`

Use this map only after exhausting the topic docs in `doc_map.md`.

## Topic query tokens
- `traceback`
- `parser`
- `status`
- `sanity_check`
- `reserved_headers`
- `harmonize`
- `fill_data`
- `get_lead`
- `plot_mqq`

## Fast source navigation
- `rg -n "<symbol_or_keyword>" src/gwaslab`
- `rg -n "error|warn|status|raise|exception" src/gwaslab/CLI/cli.py src/gwaslab/qc src/gwaslab/hm src/gwaslab/io`

## Suggested source entry points
- `src/gwaslab/CLI/cli.py` | argument parsing and stage orchestration for failure reproduction
- `src/gwaslab/g_Sumstats.py` | API wrappers where user-visible errors surface
- `src/gwaslab/io/io_preformat_input.py` | load-time schema/column parsing failures
- `src/gwaslab/qc/qc_fix_sumstats.py` | ID/CHR/POS/allele normalization issues
- `src/gwaslab/qc/qc_sanity_check.py` | range and consistency checks
- `src/gwaslab/qc/qc_reserved_headers.py` | reserved-header conflicts and dtype expectations
- `src/gwaslab/hm/hm_harmonize_sumstats.py` | harmonization status and strand/ref checks
- `src/gwaslab/hm/hm_assign_rsid.py` | rsID lookup and annotation failures
- `src/gwaslab/util/util_in_fill_data.py` | derived-stat fill logic and edge cases
- `src/gwaslab/util/util_in_get_sig.py` | lead/novel extraction edge cases
- `src/gwaslab/viz/viz_plot_mqqplot.py` | plotting failures and rendering edge cases

## Function-level behavior checks
- `pytest -q test/test_sumstats_object.py test/test_preformat_input.py`
- `pytest -q test/test_qc_and_harmonize.py test/test_target_sumstats_qc.py`
- `pytest -q test/test_get_lead_top.py test/test_viz_mqqplot.py`
- `pytest -q test/test_validate_ssf_comprehensive.py`
