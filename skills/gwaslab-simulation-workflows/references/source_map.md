# gwaslab source map: Simulation Workflows

Generated from source roots:
- `src`

Use this map only after exhausting the topic docs in `doc_map.md`.

## Topic query tokens
- `basic_check`
- `harmonize`
- `assign_rsid`
- `infer_strand`
- `clump`
- `ldsc`
- `meta_analyze`
- `simulate_sumstats`
- `liftover`

## Fast source navigation
- `rg -n "<symbol_or_keyword>" src/gwaslab`
- `rg -n "^\s+def\s+(basic_check|harmonize|clump|estimate_h2_by_ldsc|estimate_rg_by_ldsc|to_format)" src/gwaslab/g_Sumstats.py`

## Suggested source entry points
- `src/gwaslab/g_Sumstats.py` | key methods: `basic_check`, `harmonize`, `assign_rsid`, `clump`, `estimate_h2_by_ldsc`, `estimate_rg_by_ldsc`, `to_format`
- `src/gwaslab/qc/qc_fix_sumstats.py` | key functions: `_fix_ID`, `_fix_chr`, `_fix_pos`, `_fix_allele`, `_parallelize_normalize_allele`
- `src/gwaslab/qc/qc_sanity_check.py` | key functions: `_sanity_check_stats`, `_check_data_consistency`
- `src/gwaslab/hm/hm_harmonize_sumstats.py` | key functions: `check_status`, `assign_rsid_single`, `checkaf`, `_parallelize_infer_strand`
- `src/gwaslab/hm/hm_assign_rsid.py` | key functions: `_assign_rsid`, `_assign_from_lookup`, `_worker_bcf_lookup`
- `src/gwaslab/hm/hm_infer_with_af.py` | key functions: `_infer_strand_with_annotation`, `_infer_strand`
- `src/gwaslab/hm/hm_liftover_v2.py` | key function: `_liftover_variant`
- `src/gwaslab/util/util_ex_run_clumping.py` | key function: `_clump`
- `src/gwaslab/util/util_ex_ldsc.py` | key functions: `_munge_sumstats`, `_estimate_h2_by_ldsc`, `_estimate_rg_by_ldsc`
- `src/gwaslab/util/util_in_meta.py` | key function: `meta_analyze_multi`
- `src/gwaslab/util/util_in_simulate.py` | key functions: `simulate_sumstats_region`, `simulate_sumstats_global`
- `src/gwaslab/CLI/cli.py` | key function: `_process_sumstats` for end-to-end CLI workflows

## Function-level behavior checks
- `pytest -q test/test_qc_and_harmonize.py test/test_target_sumstats_qc.py`
- `pytest -q test/test_clumping.py test/test_ldsc.py`
- `pytest -q test/test_meta_analyze_multi.py test/test_simulate_sumstats.py`
- `pytest -q test/test_liftover.py test/test_rsid_to_chrpos_hdf5.py`
