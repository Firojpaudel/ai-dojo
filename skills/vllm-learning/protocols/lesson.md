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

Before choosing the action for a turn, inspect the learner's competency scores in `<workspace_root>/.vllm-learning/competencies.json`:

1. **If `intuition` or `mathematical_model` < 0.60**:
   - Focus on **The Core Block**: Physical bottleneck derivation, roofline limits, memory bandwidth vs compute bound.
2. **If `toy_implementation` or `invariant_testing` < 0.60**:
   - Focus on **The Evidence Block**: Provide interface signatures and failing tests. Learner writes the implementation.
3. **If `benchmarking_rigor` or `kernel_profiling` < 0.60**:
   - Focus on **Empirical Measurement**: Run controlled trials, profile memory/latency distributions, or perform hardware roofline derivations.
4. **If `production_tracing` < 0.60**:
   - Focus on **The Production Mapping Block**: Active upstream navigation in the current vLLM repository.
5. **If `trade_off_analysis` or `adversarial_defense` < 0.60**:
   - Focus on **The Mastery Block**: Adversarial fault injection, oral defense probe, or teach-back.

## 3. Session Pacing & Context Conservation

- **Single Interaction Anchor**: Deliver one clear conceptual invariant per conversational turn.
- **Silent State Updates**: Update `.vllm-learning/competencies.json` and `.vllm-learning/progress.md` without echoing extensive status text in chat responses.
- **Anti-Interrogation Discipline**: Do not turn the session into a rapid-fire quiz. Anchor every question in an architectural or hardware invariant.
