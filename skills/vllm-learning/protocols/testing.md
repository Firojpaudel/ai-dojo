# Systems Invariant & Correctness Testing Protocol

## 1. Testing as Executable Specification

Tests are not merely post-hoc validation; they are the executable mathematical specification of the system invariant.

## 2. Mandatory Test Dimensions

For any educational or systems implementation, include tests across these dimensions:

### A. Mathematical Invariant Tests
- Verify exact equivalence against a trusted naive reference implementation (e.g., PyTorch standard attention vs. paged attention with `torch.allclose(atol=1e-3, rtol=1e-3)`).
- Verify numerical stability under extreme logits (large negative values in causal masks).

### B. Hardware & Memory Boundary Tests
- **Non-Aligned Sequence Lengths**: Sequence lengths that are not multiples of the block size (e.g., sequence length 17 with block size 16 to test internal fragmentation).
- **Zero-Length & Single-Token Edge Cases**: Sequence length 0, prompt length 1, generation length 1.
- **Capacity Saturation & OOM Boundaries**: Fill allocator to 100% capacity; verify graceful rejection or eviction rather than unhandled panic.

### C. Concurrency & Lifetime Tests
- **Prefix Sharing (Copy-on-Write)**: Multiple requests sharing a common prefix prompt block. Verify modifications to one sequence duplicate blocks correctly without corrupting others.
- **Reference Count Invariants**: Verify block reference counts return strictly to 0 when requests finish or abort.

## 3. Test Failure Protocol

When a test fails:
1. Isolate the failing test name and exact assertion error.
2. Ask the learner: *"What invariant did this test violate?"*
3. Use the 3-Tier Hint Progression (`protocols/implementation.md`) to guide the fix.
