# gwaslab source map: Parallel and HPC

Generated from source roots:
- `src`

Use this map only after exhausting the topic docs in `doc_map.md`.

## Topic query tokens
- `threads`
- `sweep_mode`
- `parallelize`
- `assign_rsid`
- `rsid_to_chrpos`
- `clump`
- `ldsc`
- `command_runner`
- `batch`

## Fast source navigation
- `rg -n "threads|sweep_mode|parallel|worker|runner" src/gwaslab`
- `rg -n "_parallelize|_worker|_clump|_estimate_h2_by_ldsc|_estimate_rg_by_ldsc" src/gwaslab`

## Suggested source entry points
- `src/gwaslab/CLI/cli.py` | key flags: `--threads`, `--sweep-mode`, `--harmonize`
- `src/gwaslab/g_Sumstats.py` | threaded workflow methods: `basic_check`, `harmonize`, `assign_rsid`, `clump`, `estimate_h2_by_ldsc`
- `src/gwaslab/hm/hm_harmonize_sumstats.py` | key functions: `_parallelize_assign_rsid`, `_parallelize_infer_strand`, `_parallelize_check_af`
- `src/gwaslab/hm/hm_assign_rsid.py` | key functions: `_worker_bcf_lookup`, `_assign_from_lookup`
- `src/gwaslab/qc/qc_fix_sumstats.py` | key function: `_parallelize_normalize_allele`
- `src/gwaslab/util/util_ex_run_clumping.py` | key function: `_clump` (PLINK wrapper)
- `src/gwaslab/util/util_ex_ldsc.py` | key functions: `_munge_sumstats`, `_estimate_h2_by_ldsc`, `_estimate_rg_by_ldsc`
- `src/gwaslab/util/cwrapper/util_ex_command_runner.py` | shell command execution wrapper
- `src/gwaslab/util/rwrapper/util_ex_r_runner.py` | R command execution wrapper
- `src/gwaslab/util/pwrapper/util_ex_python_runner.py` | Python subprocess wrapper

## Function-level behavior checks
- `pytest -q test/test_qc_and_harmonize.py test/test_rsid_to_chrpos_hdf5.py`
- `pytest -q test/test_clumping.py test/test_ldsc.py`
- `pytest -q test/test_process_plink_input_files.py test/test_r_runner.py`
