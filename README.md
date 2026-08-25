# Pedagogical Provenance

Research code for:

**Course-Aware Ranking for Pedagogical Provenance in Medical Imaging Educational RAG**

## Overview

Course-grounded educational question answering requires more than semantic relevance. A retrieved source can be topically relevant while still being poorly aligned with the learner's current instructional position.

This repository contains the code used to evaluate **pedagogical provenance** through evidence delivery, course-aware ranking, exact instructional-source attribution, and sequence/scope control.

## Release Scope

This repository releases **source code, documentation, and two sequence-policy evaluation sets** used in the study.

Released benchmark artifacts:

- `data/benchmark/canonical_multiconcept_sequence.jsonl` — 228 canonical multi-concept sequence-policy tasks
- `data/benchmark/alternate_form_sequence.jsonl` — 96 matched alternate-surface-form sequence-policy tasks

Their SHA-256 checksums are recorded in `BENCHMARK_CHECKSUMS.sha256`.

The repository does **not** redistribute:

- course slides or lecture text
- the 1,000-task core QA benchmark, whose reference answers contain source-derived instructional text
- generated model answers
- experimental result tables
- intermediate analysis outputs
- model weights or model caches
- private validation packages

Other required local inputs are placed under `data/`. Generated outputs are written under `artifacts/`, which is ignored by Git except for its placeholder file.

## Repository Structure

```text
Pedagogical-Provenance/
├── README.md
├── requirements.txt
├── CODE_CHECKSUMS.sha256
├── configs/
├── docs/
├── data/
│   ├── benchmark/
│   ├── corpus/
│   └── external/
├── artifacts/
└── src/
    ├── attribution/
    ├── benchmark/
    ├── common/
    ├── controller/
    ├── evaluation/
    ├── external/
    ├── generation/
    ├── ranking/
    └── retrieval/
```

## Main Experimental Components

### Benchmark construction

```text
src/benchmark/build_core_benchmark_audit.py
src/benchmark/build_canonical_multiconcept_sequence_set.py
src/benchmark/build_alternate_form_sequence_set.py
```

### Retrieval

```text
src/retrieval/run_position_constrained_retrieval.py
src/retrieval/run_matched_retrieval_core.py
src/retrieval/run_advanced_retrieval.py
src/retrieval/run_rrf_lecture_slide_hybrid.py
src/retrieval/run_cross_encoder_diagnostics.py
src/retrieval/run_stronger_cross_encoder.py
src/retrieval/run_full_cross_encoder_evaluation.py
```

### Leakage-safe course-aware ranking

```text
src/ranking/run_course_position_ranker.py
```

### Matched generation

```text
src/generation/run_matched_global_position_generation.py
src/generation/merge_matched_generation_results.py
```

### Exact source attribution

```text
src/attribution/run_exact_citation_audit.py
```

The exact citation parser used by the attribution analysis is released as:

```text
src/common/citation_metrics.py
```

### Course-support control and robustness

```text
src/controller/run_course_aware_controller.py
src/controller/run_concept_held_out_evaluation.py
src/controller/run_controller_ablation.py
src/controller/run_position_controller_analysis.py
src/controller/run_controller_surface_form_robustness.py
```

### Retrieval-generation and policy analysis

```text
src/evaluation/run_retrieval_generation_linkage.py
src/evaluation/run_policy_control_analysis.py
```

### External validation

```text
src/external/run_external_course_aware_controller.py
```

## Leakage Constraint

The benchmark current course position is anchored to the target instructional location. Therefore, exact target-slide position distance would identify the target directly.

The reported leakage-safe course-aware ranker excludes:

```text
signed_position_distance
abs_position_distance
slide_distance_same_lecture
```

Its positional information is restricted to coarse lecture-level signals:

```text
same_lecture
lecture_distance
```

Cross-validation is grouped by target lecture.

## Installation

```bash
python -m venv .venv
source .venv/bin/activate
python -m pip install --upgrade pip
pip install -r requirements.txt
```

GPU-backed generation and embedding experiments require a CUDA-compatible PyTorch installation appropriate for the local system.

## Local Data

The 1,000-task core QA benchmark is expected locally at:

```text
data/benchmark/core_qa_benchmark.jsonl
```

It is not redistributed in this repository because its reference answers contain source-derived instructional text.

Two sequence-policy evaluation sets are distributed directly:

```text
data/benchmark/canonical_multiconcept_sequence.jsonl
data/benchmark/alternate_form_sequence.jsonl
```

Verify their integrity with:

```bash
sha256sum -c BENCHMARK_CHECKSUMS.sha256
```

External validation inputs, when used, are stored locally under:

```text
data/external/
```

## Generated Artifacts

Runtime outputs are written under:

```text
artifacts/
```

This directory is ignored by Git. Experimental results produced locally should not be committed to the public repository.

## Reproducibility

See:

- [`docs/EXPERIMENT_MAP.md`](docs/EXPERIMENT_MAP.md)
- [`docs/DATA_LAYOUT.md`](docs/DATA_LAYOUT.md)
- [`docs/REPRODUCIBILITY.md`](docs/REPRODUCIBILITY.md)

Some analyses consume upstream artifacts generated by earlier pipeline stages. Those dependencies are documented rather than redistributed.

## Source Integrity

SHA-256 checksums for released Python source files are recorded in:

```text
CODE_CHECKSUMS.sha256
```

Checksums for the two released sequence-policy evaluation sets are recorded in:

```text
BENCHMARK_CHECKSUMS.sha256
```

Verify both with:

```bash
sha256sum -c CODE_CHECKSUMS.sha256
sha256sum -c BENCHMARK_CHECKSUMS.sha256
```

## Citation

A formal citation entry can be added after the manuscript receives a permanent publication record.

## Contact

For questions about the code or reproducibility, please open an issue in this repository.
