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

## 3. Objective Scoring Rubric (Discrete 3-Level Scale {0, 1, 2})

Rather than unstable floating-point estimates, the agent scores each competency dimension using three discrete, observable states:

- **`0` — None**: Absent mental model, unsupported guess, non-functional code, or inability to articulate the underlying physical constraint.
- **`1` — Scaffolded**: Functional with assistance. Derives the invariant or passes tests with the help of Tier 1 or Tier 2 hints, or recalls mechanisms with minor gaps.
- **`2` — Autonomous**: Full independent mastery. Derives the invariant from first principles without hints, writes passing invariant tests, refutes adversarial traps, or navigates upstream source unassisted.

---

## 4. Single-Source-of-Truth Competency Schema (No Drifting Derived Fields)

To prevent state desynchronization, `.vllm-learning/competencies.json` stores **only the raw 12-dimensional discrete levels {0, 1, 2} and the last assessed timestamp**. Derived metrics (`mastery_status`, `weakest_dimension`, `next_best_learning_action`) are computed dynamically by the agent at runtime, never stored redundantly.

```json
{
  "concepts": {
    "autoregressive_decode_memory_bandwidth": {
      "competencies": {
        "intuition": 2,
        "mathematical_model": 2,
        "toy_implementation": 1,
        "invariant_testing": 1,
        "benchmarking_rigor": 0,
        "kernel_profiling": 0,
        "production_tracing": 0,
        "trade_off_analysis": 0,
        "debugging_isolation": 0,
        "adversarial_defense": 0,
        "teach_back": 0,
        "independence": 1
      },
      "last_assessed": "2026-09-14T01:10:00Z"
    }
  }
}
```

### Dynamic NBLA Derivation
When deciding the Next-Best-Learning-Action (NBLA):
1. Identify dimensions for the active concept where score is `0`:
   - If `intuition` or `mathematical_model` is `0` -> Execute Core Block (Q&A derivation).
   - If `toy_implementation` or `invariant_testing` is `0` -> Execute Evidence Block (Interface stub & failing tests).
   - If `production_tracing` is `0` -> Execute Production Mapping Block (Upstream code drill).
2. If all core dimensions are `1`:
   - Provide Tier 2/3 fading scaffolding to move them to `2`.
3. If all dimensions reach `2`:
   - Execute Mastery Block (Adversarial challenge & teach-back), then advance to the next stage.
