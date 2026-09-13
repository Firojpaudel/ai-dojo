# Production Mapping & Dynamic Source Grounding Protocol

## Core Purpose

Bridge the gap between theoretical models, toy implementations, and active production systems code without relying on stale, brittle, or hardcoded file paths.

---

## 1. Dynamic Runtime Source Discovery (Non-Negotiable)

Source-grounded engineering means grounded at **runtime**, not authoring time. Because production runtimes like vLLM evolve rapidly, the agent and learner must never assume static file paths or invent line numbers.

### The Dynamic Discovery Cycle
1. **Bootstrap Checkout (If Not Present)**:
   If no local clone of vLLM exists in the workspace:
   ```bash
   git clone --depth 1 https://github.com/vllm-project/vllm.git
   cd vllm && git rev-parse --short HEAD
   ```
2. **Search the Active Checkout**: Use ripgrep or grep tools to locate the target symbol or entry point in the current repository:
   ```bash
   # Example: locate the modern V1 scheduler entry point
   git grep "class .*Scheduler" vllm/v1/
   ```
3. **State Ground-Truth Metadata**: Always record:
   - **Repository & Commit Hash**: e.g., `vllm @ commit 7a8b9c...` (or current active release tag).
   - **Target File Path**: Verified in the active repository checkout (e.g., `vllm/v1/core/sched/scheduler.py`).
   - **Target Class / Function**: e.g., `Scheduler.schedule()` or `KVCacheManager`.
4. **Never Invent Line Numbers**: Direct the learner to semantic landmarks (class definitions, method names, loop invariants) rather than volatile static line ranges.

---

## 2. Mandatory Source-to-Source Triangulation Map

For every major inference mechanism covered, build and maintain this verified map:

```text
CONCEPT
├── theory / original paper
├── official documentation / RFC
├── current production source (VERIFIED at active commit)
│   ├── exact verified file path
│   └── exact class and method name
├── relevant test (executable specification in tests/)
├── relevant benchmark (measured performance in benchmarks/)
├── architectural evolution (why legacy v0 was replaced by v1, citing V1 design RFCs / docs)
└── underlying GPU/hardware primitive (HBM, SRAM, NVLink, CUDA stream)
```

---

## 3. Active Navigation Directive

Never paste large dumps of production code with passive lectures. Enforce active navigation:

1. **Direct the Learner**:
   - *"Grep for `class <TargetClass>` in `<subsystem_dir>`."*
   - *"Open `<verified_file>` and locate method `<target_method>`."*
   - *"Inspect the loop handling preemption or memory exhaustion."*
2. **Elicit Hypothesis Before Explaining**:
   - *"Before I explain it, what system invariant does this check enforce when free blocks reach zero?"*
3. **Analyze Complexity Delta**:
   - Compare the production implementation against the learner's toy model: why did production add complexity? (e.g., chunked prefill co-scheduling, multi-worker coordination, CUDA graph capture compatibility).
4. **Engine Generation Awareness**:
   - Strictly distinguish:
     - **Paper Architecture**: The algorithmic concept (e.g., PagedAttention 2023 SOSP paper).
     - **Historical vLLM (V0)**: Legacy Ray worker, asyncio scheduler, discrete prefill/decode batches (deprecated/deleted).
     - **Modern vLLM (V1)**: Multiprocessing core, unified block management, chunked prefill by default.
