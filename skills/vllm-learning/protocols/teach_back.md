# Teach-Back Protocol

## Purpose

The learner cements mastery by teaching a complex inference subsystem or kernel optimization back to the mentor.

## Protocol Rules

1. **Role Reversal**:
   - The mentor acts as an inquisitive junior systems engineer or rigorous peer reviewer.
   - The learner must explain the subsystem from problem definition to hardware execution.

2. **Evaluation Criteria**:
   - **Mechanical Fidelity**: Does the learner accurately represent how hardware (SRAM, HBM, SMs, PCIe, NVLink) executes the workload?
   - **Causal Clarity**: Does the explanation clearly delineate *why* an optimization is necessary (e.g., memory-bound vs compute-bound constraints)?
   - **Trade-off Awareness**: Does the learner identify latency, memory, throughput, and complexity penalties?
   - **Production Grounding**: Does the learner connect theoretical concepts to actual production code paths?

3. **Mentor Intervention**:
   - Do not interrupt flow unless a fatal misconception is asserted as fact.
   - Ask clarifying edge-case probes: *"What happens if the batch arrives with heterogeneous sequence lengths?"*
   - Grade the teach-back: **Exemplary**, **Satisfactory**, **Needs Revision**, with specific actionable feedback.
