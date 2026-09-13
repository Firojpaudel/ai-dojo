# Adversarial Defense & Bug Injection Protocol

## 1. Purpose

True systems competence is demonstrated by diagnosing subtle failures, detecting misleading benchmarks, and defending architectural designs against adversarial scrutiny.

## 2. The Three Adversarial Exercises

### Exercise A: The Injected Defect (Fault Isolation)
The agent provides the learner with an almost-correct implementation containing a realistic systems bug:
- **Off-by-One in Block Allocation**: Allocator drops the tail token when sequence length is an exact multiple of block size.
- **Race Condition in Batch Scheduler**: Mutating active sequence list during iteration without a snapshot.
- **Stale Block Reference**: Allocating physical blocks without resetting dirty memory buffers.
- *Learner Objective*: Write a failing test that isolates the bug, identify the broken invariant, and fix it.

### Exercise B: The Misleading Benchmark (Threats to Validity)
The agent presents a plausible-looking benchmark claim with a fatal methodological flaw:
- Timing asynchronous CUDA kernel launches without `torch.cuda.synchronize()`.
- Measuring TTFT on pre-cached prompts without flushing GPU L2 cache.
- Reporting average latency under heavy tail latency (p99) collapse.
- *Learner Objective*: Dissect why the conclusion is invalid and specify the corrected methodology.

### Exercise C: The False Optimization Challenge
The agent makes a plausible but flawed performance assertion:
- *"We can eliminate internal KV cache fragmentation by using a block size of 1 token."*
- *"We should use FP8 for all KV cache storage regardless of head dimension or model calibration."*
- *Learner Objective*: Refute the claim using hardware constraints (e.g. page table overhead, memory coalescing penalties, quantization noise).

## 3. Defense Scoring Rubric
- **Grounded in Invariants (1.0)**: Uses memory bandwidth, cache lines, or code paths to refute/diagnose.
- **Surface Plausibility (0.5)**: Correctly senses something is wrong but cannot articulate the hardware/software mechanism.
- **Deceived (0.0)**: Accepts the bug, false optimization, or bad benchmark without objection.
