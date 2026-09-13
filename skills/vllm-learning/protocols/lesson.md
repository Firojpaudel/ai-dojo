# Adaptive Lesson Execution Protocol (4-Block Architecture)

## 1. Non-Linear Execution Principle

Do NOT force a mechanical 22-step checklist. Real systems mentorship adapts dynamically to the learner's weakest competency axis.
Every lesson executes within a modular **4-Block Adaptive Framework**:

```text
┌─────────────────────────────────────────────────────────────┐
│ 1. THE CORE BLOCK                                           │
│    Bottleneck -> Physical Invariant -> Source Target ->     │
│    Single Diagnostic Question (ask_question or chat block)  │
└──────────────────────────────┬──────────────────────────────┘
                               ▼
┌─────────────────────────────────────────────────────────────┐
│ 2. THE EVIDENCE BLOCK                                       │
│    Toy Model Stub -> Invariant Tests -> Empirical Run       │
│    (or Roofline Calculation if GPU Unavailable)             │
└──────────────────────────────┬──────────────────────────────┘
                               ▼
┌─────────────────────────────────────────────────────────────┐
│ 3. THE PRODUCTION MAPPING BLOCK                             │
│    Dynamic Upstream Target -> Active Drill -> Delta         │
└──────────────────────────────┬──────────────────────────────┘
                               ▼
┌─────────────────────────────────────────────────────────────┐
│ 4. THE MASTERY BLOCK                                        │
│    Adversarial Probe -> Teach-Back -> Competency Update     │
└─────────────────────────────────────────────────────────────┘
```

## 2. Next-Best-Learning-Action (NBLA) Selection

Inspect the learner's discrete competency levels in `<workspace_root>/.vllm-learning/competencies.json` and follow the dynamic NBLA derivation rules in [protocols/state_tracking.md](state_tracking.md) Section 4.

## 3. Session Pacing & Context Conservation

- **Single Interaction Anchor**: Deliver one clear conceptual invariant per conversational turn.
- **Silent State Updates**: Update `.vllm-learning/competencies.json` and `.vllm-learning/progress.md` without echoing extensive status text in chat responses.
- **Anti-Interrogation Discipline**: Do not turn the session into a rapid-fire quiz. Anchor every question in an architectural or hardware invariant.
