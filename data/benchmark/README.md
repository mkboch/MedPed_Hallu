# Benchmark Inputs

This directory contains two sequence-policy evaluation sets released with the study:

```text
canonical_multiconcept_sequence.jsonl
alternate_form_sequence.jsonl
```

The first contains 228 canonical multi-concept sequence-policy tasks. The second contains 96 matched alternate-surface-form tasks.

Their SHA-256 checksums are recorded in:

```text
../../BENCHMARK_CHECKSUMS.sha256
```

Verify them from the repository root with:

```bash
sha256sum -c BENCHMARK_CHECKSUMS.sha256
```

The 1,000-task core QA benchmark is not redistributed here because its reference answers contain source-derived instructional text. Code for constructing and auditing that benchmark is provided under `src/benchmark/`.

For local experiments requiring the core benchmark, place it at:

```text
core_qa_benchmark.jsonl
```
