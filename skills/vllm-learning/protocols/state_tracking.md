# Dynamic State Tracking & Competency Evaluation Protocol

## 1. Decoupled Workspace State Principle

Learner state must **NEVER** live inside the distributed skill package directory (e.g., inside `.agents/skills/vllm-learning/`). If state lived inside the package, running `npx skills add` to update the skill would clobber the learner's history, and global installs (`-g`) would collide across different projects.

### Workspace State Location
All mutable learner state is stored locally in the active workspace root under:
```text
<workspace_root>/.vllm-learning/
├── competencies.json    # 12-factor continuous competency scores per concept
├── misconceptions.json  # Diagnosed mental model bugs and ground-truth invariants
└── progress.md          # High-level narrative and active curriculum stage
```

If `.vllm-learning/` does not exist when a session begins, the agent initializes it from the default schemas shipped with the skill. Updating or reinstalling the skill never touches this workspace directory.

---

## 2. When the Agent Updates State

State updates must not occur on every conversational message (to avoid file thrashing and context noise). The agent updates state strictly at these **five checkpoint triggers**:

| Event Trigger | Associated Competency Axes | Target File |
| :--- | :--- | :--- |
| **Q&A Session Completed** (`protocols/qa_session.md`) | `intuition`, `mathematical_model` | `.vllm-learning/competencies.json` |
| **Code & Invariant Tests Executed** (`protocols/testing.md`) | `toy_implementation`, `invariant_testing` | `.vllm-learning/competencies.json` |
| **Benchmark / Roofline Run** (`protocols/benchmarking.md`) | `benchmarking_rigor`, `kernel_profiling` | `.vllm-learning/competencies.json` |
| **Upstream Code Drill** (`protocols/production_mapping.md`) | `production_tracing`, `trade_off_analysis` | `.vllm-learning/competencies.json` |
| **Adversarial Challenge / Defense** (`protocols/adversarial_defense.md`) | `debugging_isolation`, `adversarial_defense`, `teach_back` | `.vllm-learning/competencies.json` |
| **Systems Misconception Diagnosed** | Records transcript quote & invariant | `.vllm-learning/misconceptions.json` |

---

## 3. Objective Scoring Rubric (Continuous Scale 0.00 – 1.00)

The agent evaluates learner evidence against these concrete anchors:

- **0.00 – 0.20 (No Grounding / Guess)**: Learner makes an unsupported guess, refuses derivation, or demonstrates complete absence of the physical mental model.
- **0.21 – 0.50 (Surface / Fragile)**: Learner recalls syntax or names, but cannot explain why the mechanism works under physical/hardware constraints.
- **0.51 – 0.70 (Working with Scaffolding)**: Learner derives the invariant or writes passing code with the help of Tier 1 or Tier 2 hints.
- **0.71 – 0.89 (Autonomous Mastery)**: Learner derives the invariant from scratch, passes all edge-case tests, or points to upstream source without hints.
- **0.90 – 1.00 (Adversarial Defense)**: Learner refutes an adversarial counter-claim, isolates an injected bug, or teaches the concept back flawlessly.

---

## 4. Single-Source-of-Truth Competency Schema (No Drifting Derived Fields)

To prevent state desynchronization, `.vllm-learning/competencies.json` stores **only the raw 12-dimensional scores and the last assessed timestamp**. Derived metrics (`mastery_status`, `weakest_dimension`, `next_best_learning_action`) are computed dynamically by the agent at runtime, never stored redundantly.

```json
{
  "concepts": {
    "autoregressive_decode_memory_bandwidth": {
      "competencies": {
        "intuition": 0.80,
        "mathematical_model": 0.70,
        "toy_implementation": 0.00,
        "invariant_testing": 0.00,
        "benchmarking_rigor": 0.00,
        "kernel_profiling": 0.00,
        "production_tracing": 0.00,
        "trade_off_analysis": 0.00,
        "debugging_isolation": 0.00,
        "adversarial_defense": 0.00,
        "teach_back": 0.00,
        "independence": 0.60
      },
      "last_assessed": "2026-09-14T01:10:00Z"
    }
  }
}
```

### Dynamic NBLA Derivation
When deciding the Next-Best-Learning-Action (NBLA):
1. Find the active concept's dimension with the lowest score ($< 0.70$).
2. If `intuition` or `mathematical_model` is lowest -> Execute Core Block (Q&A).
3. If `toy_implementation` or `invariant_testing` is lowest -> Execute Evidence Block (Coding).
4. If `production_tracing` is lowest -> Execute Production Mapping Block (Source Drill).
5. If all dimensions $\ge 0.70$ and `adversarial_defense` $< 0.90$ -> Execute Mastery Block (Adversarial Challenge).
