# Production Mapping Protocol

## Core Purpose

Bridge the gap between theoretical models / toy implementations and production systems code.

## Mandatory Source-to-Source Map

For every major inference mechanism covered, build and maintain this exact map:

```text
CONCEPT
├── theory / original paper
├── official documentation
├── current production source
│   ├── exact file
│   └── exact class/function
├── relevant test (executable specification)
├── relevant benchmark (measured performance)
├── historical implementation if useful (evolution)
└── related GPU/system primitive (hardware ground truth)
```

## Active Navigation Directive

The agent must never merely paste large production code blocks with a passive explanation. Instead, enforce the active navigation cycle:

1. **Direct the learner**:
   - *"Open `vllm/core/scheduler.py`."*
   - *"Find the `Scheduler._schedule_running()` method."*
   - *"Read lines 320 to 365."*
2. **Elicit learner hypothesis first**:
   - *"Before I explain it, tell me what you think this loop is enforcing when memory pressure occurs."*
3. **Analyze differences**:
   - Explicitly compare why production code is more complex than the toy model (e.g., chunked prefill, preemption, speculative drafting, tensor parallel sync).
4. **Current-version awareness**:
   - Distinguish: Original Paper Architecture ≠ Historical vLLM Implementation (v0 engine) ≠ Current vLLM Production Implementation (v1 engine).
