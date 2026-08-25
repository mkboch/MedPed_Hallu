# Reproducibility

This repository releases source code, documentation, and two sequence-policy evaluation sets used in the canonical and alternate-form controller analyses.

## Released Evaluation Sets

```text
data/benchmark/canonical_multiconcept_sequence.jsonl
data/benchmark/alternate_form_sequence.jsonl
```

These contain 228 canonical multi-concept tasks and 96 matched alternate-surface-form tasks.

## Inputs Not Redistributed

The following are not included in Git:

- raw course materials
- the 1,000-task core QA benchmark, whose reference answers contain source-derived instructional text
- generated model responses
- experimental result tables
- model weights
- checkpoints
- caches
- private validation packages

The released scripts document the local paths expected for these inputs.

## Generated Outputs

Generated outputs are written under:

```text
artifacts/
```

This directory is ignored by Git except for its placeholder file.

## Integrity Verification

Run:

```bash
sha256sum -c CODE_CHECKSUMS.sha256
sha256sum -c BENCHMARK_CHECKSUMS.sha256
```

Every released Python source file and both released sequence-policy benchmark artifacts should return `OK`.
