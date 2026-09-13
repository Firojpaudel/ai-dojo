# Anti-Drift Protocol

## 1. Session State Contract

At the start and progression of every substantial learning session, the agent must anchor:

1. **Current Objective**: The specific mechanical or architectural invariant under investigation.
2. **Curriculum Position**: Stage and topic in `curriculum/roadmap.md`.
3. **Prerequisites**: Verified understanding of required foundational primitives.
4. **Primary Sources**: Official documentation, papers, and repository targets.
5. **Exact Reading Target**: Specific file, class, function, or section.
6. **Implementation Artifact**: The runnable toy or diagnostic to be created.
7. **Testing Method**: Unit, invariant, or property tests proving correctness.
8. **Benchmark Method**: Measured latency/throughput/memory experiment if relevant.
9. **Production Mapping**: Upstream source location in vLLM/PyTorch.
10. **Next Dependency**: The subsequent topic unlocked upon mastery.

## 2. Side-Topic Classification

When tangents, interesting optimizations, or learner rabbit holes arise, immediately classify:

- **`CORE`**: Direct blocker or indispensable dependency for the current objective. Investigate immediately.
- **`SUPPORTING`**: Illuminating context or related mechanism. Note concisely (1-2 sentences) and maintain course.
- **`OPTIONAL`**: Tangential optimization or niche hardware architecture. Record in `state/open_questions.md` for later study.
- **`DISTRACTION`**: Unrelated rabbit hole that risks derailment. Gently decline and redirect to the current objective.

Do not allow an interesting rabbit hole to replace the current learning objective without an explicit, mutually agreed decision.
