# gwaslab source map: Build and Install

Generated from source roots:
- `src`

Use this map only after exhausting the topic docs in `doc_map.md`.

## Topic query tokens
- `install`
- `cli`
- `version`
- `preformat`
- `infer_build`
- `liftover`
- `download_ref`
- `path_manager`

## Fast source navigation
- `rg -n "<symbol_or_keyword>" src/gwaslab`
- `rg -n "^(def|class)\s+" src/gwaslab/CLI/cli.py src/gwaslab/qc/qc_build.py src/gwaslab/hm/hm_liftover_v2.py src/gwaslab/bd/bd_download.py`

## Suggested source entry points
- `src/gwaslab/CLI/cli.py` | key functions: `_cmd_version`, `_process_sumstats`, `main`
- `src/gwaslab/__main__.py` | package entrypoint for `python -m gwaslab`
- `src/gwaslab/__init__.py` | top-level API exports used in smoke checks
- `src/gwaslab/io/io_preformat_input.py` | key function: `_preformat` for first-load parsing
- `src/gwaslab/bd/bd_download.py` | key functions: `check_available_ref`, `download_ref`, `get_path`
- `src/gwaslab/qc/qc_build.py` | key functions: `_process_build`, `_set_build`, `_check_build`
- `src/gwaslab/hm/hm_liftover_v2.py` | key function: `_liftover_variant`
- `src/gwaslab/bd/bd_sumstats_formats.py` | key function: `detect_sumstats_format`

## Function-level behavior checks
- `pytest -q test/test_cli.py test/test_path_manager.py`
- `pytest -q test/test_preformat_input.py test/test_infer_build_and_hapmap3.py`
- `pytest -q test/test_liftover.py`
