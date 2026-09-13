# Adversarial Challenge Record

## 1. Challenge Metadata
- **Challenge ID**: ADV-`[ID]`
- **Type**: `[Injected Defect | Misleading Benchmark | False Optimization]`
- **Target Concept**: `[e.g. Block Space Allocation | CUDA Stream Timing | Cache Coalescing]`
- **Difficulty**: `[Beginner | Intermediate | Senior Systems]`

## 2. The Artifact Under Scrutiny
`[Provide the broken code block, misleading benchmark summary, or architectural assertion here]`

## 3. The Broken Invariant (Hidden from Learner Initially)
`[The underlying physical, mathematical, or concurrency invariant violated]`

## 4. Learner Evaluation Rubric
- **Level 1 (Detection)**: Learner recognizes that the behavior or claim is flawed.
- **Level 2 (Isolation)**: Learner pinpoints the exact line, counter, or assumption at fault.
- **Level 3 (Correction & Proof)**: Learner provides the corrected implementation or experiment proving the flaw.

## 5. Debrief & State Update
- **Outcome**: `[Passed | Remediation Required]`
- **Competency Impact**: Update `debugging_isolation` or `adversarial_defense` in `state/competencies.json`.
