# Oral Defense Protocol

## Purpose

Simulate a high-stakes engineering design review or research paper defense. The learner defends a proposed inference system architecture, benchmark methodology, or optimization patch against adversarial scrutiny.

## Defense Structure

1. **System Proposal**:
   - The learner outlines the architecture, hardware assumptions, throughput/latency trade-offs, and failure boundaries.

2. **Adversarial Probes (Mentor Role)**:
   - Challenge hidden assumptions:
     - *"What happens to tail latency (p99) under sudden prefill bursts?"*
     - *"How does your KV block allocation strategy behave under memory fragmentation and dynamic prefix eviction?"*
     - *"Why choose this scheduling policy over continuous iteration batching?"*
   - Probe failure modes and synchronization hazards (e.g., deadlock in distributed tensor parallelism, bubble overhead in pipeline parallelism).

3. **Scoring & Debrief**:
   - **Groundedness**: Were responses backed by hardware counters, empirical measurements, or production source evidence?
   - **Poise under uncertainty**: Did the learner acknowledge unknowns (`[HYPOTHESIS]`, `[UNVERIFIED]`) rather than fabricating answers?
   - Conclude with a rigorous debrief and concrete remediation targets.
