# Dynamic State Tracking & Competency Evaluation Protocol

## 1. Zero Hardcoding Principle

The agent must NEVER rely on static or pre-populated state. All competency scores, diagnosed misconceptions, and progress entries must be **dynamically evaluated, computed, and recorded** in real time during the apprenticeship.

All file paths recorded in state documents must be **strictly relative to the workspace root** (e.g. `./level0_naive/naive_generator.py`, `./state/competencies.json`).

---

## 2. When the Agent Updates State

State updates must not occur on every conversational message (to avoid file thrashing and token waste). The agent updates state immediately following these **five checkpoint triggers**:

| Event Trigger | Associated Competency Axes | Target File |
| :--- | :--- | :--- |
| **Modal Q&A Completed** (`protocols/qa_session.md`) | `intuition`, `mathematical_model` | `state/competencies.json` |
| **Code & Tests Executed** (`protocols/testing.md`) | `toy_implementation`, `invariant_testing` | `state/competencies.json` |
| **Benchmark / Roofline Run** (`protocols/benchmarking.md`) | `benchmarking_rigor`, `kernel_profiling` | `state/competencies.json` |
| **Upstream Code Drill** (`protocols/production_mapping.md`) | `production_tracing`, `trade_off_analysis` | `state/competencies.json` |
| **Adversarial Challenge / Defense** (`protocols/adversarial_defense.md`) | `debugging_isolation`, `adversarial_defense`, `teach_back` | `state/competencies.json` |
| **Systems Misconception Diagnosed** | Appends new entry with remediation | `state/misconceptions.json` |

---

## 3. Objective Scoring Rubric (Continuous Scale 0.00 – 1.00)

The agent evaluates learner evidence using this deterministic rubric:

- **0.00 – 0.20 (No Grounding / Guess)**: Learner makes an unsupported guess, refuses derivation, or demonstrates complete absence of the physical mental model.
- **0.21 – 0.50 (Surface / Fragile)**: Learner recalls syntax or names, but cannot explain why the mechanism works under physical/hardware constraints.
- **0.51 – 0.70 (Working with Scaffolding)**: Learner derives the invariant or writes passing code with the help of Tier 1 or Tier 2 hints.
- **0.71 – 0.89 (Autonomous Mastery)**: Learner derives the invariant from scratch, passes all edge-case tests, or points to upstream source without hints.
- **0.90 – 1.00 (Adversarial Defense)**: Learner refutes an adversarial counter-claim, isolates an injected bug, or teaches the concept back flawlessly.

---

## 4. Agent Operational Procedure for Updating State

### Step A: Read Existing State
At session start or before an assessment, the agent inspects:
- `state/competencies.json`
- `state/misconceptions.json`
- `state/progress.md`

### Step B: Dynamically Inject or Update Concept
When a learner begins exploring a concept (e.g. `autoregressive_decode_memory_bandwidth`), the agent creates or updates the entry dynamically in `state/competencies.json` using its file writing tools:

```json
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
  "mastery_status": "in_progress",
  "weakest_dimension": "toy_implementation",
  "next_best_learning_action": "implement_toy_model",
  "last_assessed": "2026-09-14T01:10:00Z"
}
```

### Step C: Logging a Misconception
When a learner response demonstrates a flawed physical model (e.g. equating PagedAttention blocks with OS 4KB pages):
1. The agent assigns an ID: `MISC-[NNN]`.
2. Appends to `diagnosed_misconceptions` in `state/misconceptions.json`:
   - `concept`: The active concept key.
   - `category`: `physical_impossibility`, `asymptotic_fallacy`, `hardware_misalignment`, or `historical_obsolescence`.
   - `misconception`: Exact flawed assertion made by the learner.
   - `ground_truth_invariant`: The physical or software law.
   - `evidence`: Transcript quote from the learner.
   - `remediation_action`: Specific derivation or experiment assigned.
   - `status`: Set to `"UNRESOLVED"`.
3. When the learner later proves mastery of the invariant, the agent updates `status` to `"RESOLVED"`.

### Step D: Updating High-Level Narrative (`state/progress.md`)
The agent writes a human-readable summary reflecting:
- Current active stage and relative directory (e.g., `./level0_naive/`).
- Weakest dimension and computed Next-Best-Learning-Action.
- Count of unresolved misconceptions.
