# Mastery Exam Protocol

## Objective

A formal checkpoint administered before advancing between curriculum stages in the apprenticeship.

## Gate Requirements

The learner must pass all three dimensions before a stage is marked `[MASTERED]`:

1. **First-Principles Derivation**:
   - Derive the mathematical or mechanical bottleneck from scratch without referencing notes.
   - Example: Derive arithmetic intensity and memory traffic for FlashAttention vs. Standard Attention, or KV cache bytes per token across layers.

2. **Toy Model & Invariant Verification**:
   - Write or critique a minimal, standalone Python/C++/CUDA implementation exposing the core mechanism.
   - Run tests demonstrating correctness under edge conditions (e.g., sequence length not multiple of block size, concurrency conflicts, prefill/decode boundary).

3. **Production Grounding**:
   - Point to the exact current production files, classes, and functions in vLLM/PyTorch where this mechanism lives.
   - Explain why the production implementation diverges from the toy model or original paper (e.g., chunked prefill, CUDA graphs, pinned memory allocation).

## Exam Procedure

1. Present the problem scenario.
2. Pose the first core challenge and pause.
3. Assess the response against the evaluation taxonomy (`protocols/qa_session.md`).
4. If a fundamental misconception is discovered, abort graduation and open a targeted remediation module.
5. Record the outcome in `state/progress.md`.
