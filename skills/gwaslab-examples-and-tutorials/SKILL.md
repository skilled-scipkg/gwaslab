---
name: gwaslab-examples-and-tutorials
description: Use this skill to route users to the right GWASLab notebooks/examples and convert notebook-style workflows into compact, runnable Python or CLI scripts.
---

# gwaslab: Examples and Tutorials

## High-Signal Playbook
### Route Conditions
- Use this skill when the user asks for an example, walkthrough, or "show me how" workflow.
- Route to `gwaslab-getting-started` for first-run basics.
- Route to `gwaslab-simulation-workflows` for production QC/harmonization pipelines.
- Route to `gwaslab-analysis-and-output` for deep plot customization.

### Triage Questions
- What task family: loading, QC, harmonization, utility, visualization, or reference management?
- Does the user need notebook guidance or script/CLI-ready commands?
- Are they using toy data or full-scale cohort files?
- Which genome build and reference assets are available?
- Is reproducibility (fixed paths/seeds/versions) required?
- Do they want minimal runnable snippets or full tutorial parity?

### Canonical Workflow
1. Select the smallest matching example set under `examples/` by task domain (`examples/1_main_tutorial`, `3_standardization`, `4_harmonization`, `7_visualization`).
2. Pair notebook example with its docs counterpart (`docs/tutorial_v4.md` and topic docs) before extracting commands.
3. Convert notebook cells into ordered script blocks: import, load, QC/harmonize, output.
4. Replace notebook-only assumptions (absolute paths, hidden state) with explicit local paths/arguments.
5. Add one verification checkpoint (shape, lead count, output files) to confirm parity.
6. If behavior diverges from docs, escalate to skill `references/source_map.md` and targeted source files.

### Minimal Working Example
```python
# Notebook-to-script skeleton
import gwaslab as gl

s = gl.Sumstats("examples/0_sample_data/toy_data/dirty_sumstats.tsv", fmt="gwaslab", other=["NOTE"])
s.basic_check(remove=True, remove_dup=True, verbose=False)
lead = s.get_lead(sig_level=5e-8)
s.to_format("toy_clean", fmt="gwaslab")
print(f"n_variants={len(s.data)} n_lead={len(lead)}")
```

```bash
# Equivalent quick CLI pattern
gwaslab --input examples/0_sample_data/toy_data/dirty_sumstats.tsv --fmt gwaslab --qc --remove --remove-dup --out toy_clean --to-fmt gwaslab
```

### Pitfalls and Fixes
- Notebook uses hidden previous-cell state: rewrite as top-to-bottom script with explicit imports and object creation.
- Example paths are environment-specific: replace with repo-relative or user-supplied paths.
- Tutorial-scale commands are too slow for debugging: use `nrows` or toy datasets first.
- Mixed-version notebooks cause API mismatch: verify against current docs (`docs/tutorial_v4.md`, `docs/CLI.md`).
- Reference-dependent examples fail offline: validate required `gl.get_path(...)` assets early.

### Convergence and Validation Checks
- Script runs end-to-end in a fresh process (no notebook state dependence).
- Core outputs (cleaned file, lead table, plot artifact) are created deterministically.
- Row counts and lead counts are plausible relative to input and thresholds.
- CLI and API variants produce consistent high-level results.

## Scope
- Fast retrieval and adaptation of GWASLab examples/tutorials.
- Emphasis on reusable script patterns over notebook narration.

## Primary documentation references
- `docs/tutorial_v4.md`
- `docs/CLI.md`
- `docs/CLIWorkflowExamples.md`
- `docs/standardization_workflow.md`
- `docs/harmonization_workflow.md`
- `docs/visualization_mqq.md`
- `docs/visualization_regional.md`

## Tutorials and examples
- `examples/1_main_tutorial/tutorial_v4.ipynb`
- `examples/2_input_output/format_load_save.ipynb`
- `examples/3_standardization/standardization_workflow.ipynb`
- `examples/4_harmonization/harmonization_workflow.ipynb`
- `examples/7_visualization/visualization_mqq.ipynb`
- `examples/7_visualization/visualization_regional.ipynb`
- `examples/7_visualization/visualization_stacked_mqq.ipynb`

## Workflow
- Start with docs + matching examples.
- Use `references/doc_map.md` for additional topic examples.
- Escalate to source only for behavior mismatches.

## Source entry points for unresolved issues
- `src/gwaslab/g_Sumstats.py`
- `src/gwaslab/CLI/cli.py`
- `src/gwaslab/util/util_in_fill_data.py`
- `src/gwaslab/util/util_in_get_sig.py`
- `src/gwaslab/io/io_to_formats.py`
- `src/gwaslab/viz/viz_plot_mqqplot.py`
- `src/gwaslab/viz/viz_plot_regional2.py`
- `src/gwaslab/viz/viz_plot_stackedregional.py`
- Prefer targeted search: `rg -n "<symbol_or_keyword>" src/gwaslab`
