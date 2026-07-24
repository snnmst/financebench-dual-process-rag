# Thinking Fast and Slow in Finance — Data & Code Repository

Supporting data, prompts, and evaluation outputs for:

> Muştu, S., & Altun, H. O. (2026). *Thinking Fast and Slow in Finance: A
> Dual-Process Retrieval-Augmented Generation Architecture for
> Automated Financial Document Auditing
> *Information Systems Frontiers*.

This work is derived from the first author's Master's thesis at the
Boğaziçi University Institute for Data Science and Artificial Intelligence.

## What this repository contains

| Path | Description |
|---|---|
| `data/financebench_103_questions.xlsx` | The 103-question FinanceBench evaluation subset (document, query, ground truth) |
| `data/system1_standalone_outputs.csv` | Per-query System-1 verdicts, tokens, and latency (standalone ablation, Table 1 left column) |
| `data/full_pipeline_outputs.xlsx` | Per-query final verdicts for the deployed cascade, all 103 questions (Table 1 right column) |
| `data/full_pipeline_outputs_nones.xlsx` | The subset of escalated queries that returned a transient provider (API) error on the first pass, before resubmission (Section 3.4, "Phase 1" unresolved cases) |
| `data/error_taxonomy_full.csv` | Category label and rationale for all 103 questions (error category populated for the non-exact outputs only; Table 2) |
| `data/baseline_measurements/` | Raw per-query token/latency logs for the dedicated System-1-only and System-2-only baseline runs (Table 3/4, Section 4.3) — *(confirm this folder is included; see note below)* |
| `json_files.zip` | Raw MinerU document-parsing output (JSON, one file per source filing), required to reproduce the retrieval/extraction pipeline |
| `code/` | Pipeline / orchestration code |
| `prompts/` | Verbatim system prompts for System-1 and the three System-2 agents (Extractor, Auditor, Judger) |

> **Note:** `full_pipeline_outputs_nones.xlsx` currently lists 24 affected
> questions; Section 3.4 of the paper states 23. Please reconcile this
> before creating the release — whichever number is correct should match
> exactly between the paper and this file.

## Relationship to the published tables

- **Table 1** (accuracy distribution) is computed from `system1_standalone_outputs.csv` and `full_pipeline_outputs.xlsx`.
- **Table 2** (error taxonomy) is computed from `error_taxonomy_full.csv`.
- **Table 3 / Table 4** (cost analysis) are computed from the files in `data/baseline_measurements/` plus the aggregate columns in `full_pipeline_outputs.xlsx`.
- **Section 3.4** (two-phase evaluation protocol) corresponds to `full_pipeline_outputs_nones.xlsx` (the queries resubmitted in Phase 2).
- **Appendix A** of the thesis corresponds to `prompts/`.
- `json_files.zip` is a preprocessing input (MinerU output), not an evaluation output — it is provided for end-to-end reproducibility of the retrieval pipeline itself.

## Data source

The underlying questions and ground-truth answers originate from the public
**FinanceBench** benchmark (Islam et al., 2023,
[arXiv:2311.11944](https://arxiv.org/abs/2311.11944)). This repository
redistributes only the 103-question subset actually evaluated in this study,
together with **new** annotations (verdicts, error categories, cost
measurements) produced by the authors.

## Reproducibility notes

- Verdicts follow the four-way scheme defined in the paper: Exact Match (EM),
  Partial Match (PM), Correct Rejection (CR), Incorrect (INC).
- Two evaluation passes are distinguished for full-pipeline outputs
  (`phase` column: `1` = initial pass, `2` = resubmission pass after a
  transient provider error) — see Section 3.4 of the paper.
- Token and latency figures are self-reported by the pipeline's logging
  layer and were not independently re-measured after the fact.

## License

- Code and prompts (`prompts/`, any scripts): MIT License — see `LICENSE`.
- Data files (`data/`): Creative Commons Attribution 4.0 International
  (CC BY 4.0). Please cite the paper above (and the original FinanceBench
  paper, for the questions/ground truth) if you reuse this data.

## Citation

See `CITATION.cff`, or cite as:

```
Muştu, S., & Altun, H. O. (2026). Thinking Fast and Slow in Finance: A
Dual-Process Retrieval-Augmented Generation Architecture with Multi-Agent
Verification for Automated SEC Filing Analysis [Data set and code].
Zenodo. https://doi.org/10.5281/zenodo.XXXXXXX
```

*(Replace the DOI above with the one assigned by Zenodo after archiving
this repository — see the badge/link at the top of the GitHub repo once
created.)*
