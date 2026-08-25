# Local Data and Artifact Layout

The public repository includes two sequence-policy evaluation sets. Raw course materials, the 1,000-task core QA benchmark, generated model outputs, and experimental result tables are not distributed here.

## Course Corpus

Place the local slide corpus at:

```text
data/corpus/slide_corpus_final.jsonl
```

The corpus is not tracked by Git.

## Core QA Benchmark

Place the 1,000-task core QA benchmark at:

```text
data/benchmark/core_qa_benchmark.jsonl
```

Expected fields include:

```text
task_id
task_type
question
reference_answer
target_doc_id
evidence_doc_ids
metadata
```

The core QA benchmark is not redistributed in this repository because its reference answers contain source-derived instructional text.

## Released Sequence-Policy Evaluation Sets

The following artifacts are tracked directly in Git:

```text
data/benchmark/canonical_multiconcept_sequence.jsonl
data/benchmark/alternate_form_sequence.jsonl
```

They contain 228 canonical multi-concept tasks and 96 matched alternate-surface-form tasks, respectively.

Verify their integrity with:

```bash
sha256sum -c BENCHMARK_CHECKSUMS.sha256
```

## External Validation Inputs

External validation inputs, when used, are placed locally under:

```text
data/external/
```

## Generated Artifacts

Generated outputs belong under:

```text
artifacts/
```

The directory is ignored by Git except for its placeholder file.
