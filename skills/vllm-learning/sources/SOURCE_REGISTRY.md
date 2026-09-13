# Systems & Inference Primary Source Registry

Canonical primary sources for the AI systems apprenticeship. Secondary sources serve discovery only; all technical claims must trace back to these primary repositories, documentation, and landmark papers.

---

## 1. Inference Engines & Production Runtimes

### vLLM (Primary Laboratory)
- **Repository**: `https://github.com/vllm-project/vllm`
- **Current Production Architecture**: V1 Engine (`vllm/v1/...`). 
- **Critical Subsystems**:
  - `vllm/v1/core/sched/`: V1 iteration-level scheduler, dynamic scheduling, token budgeting.
  - `vllm/v1/core/kv_cache_manager.py` / Block Managers: Unified KV block allocation, logical-to-physical block tables.
  - `vllm/v1/worker/`: Model runner execution loop, GPU worker process coordination.
  - `vllm/attention/`: Attention backend selectors and custom attention ops.
  - `csrc/`: Custom CUDA and C++ kernels (PagedAttention, quantization kernels).
- **Historical Context**: Legacy V0 architecture (`vllm/core/`) was deprecated and frozen; do not reference V0 files for modern behavior.

---

## 2. Hardware Architecture & Runtime Ecosystems

### NVIDIA CUDA & GPU Architecture
- **CUDA Programming Guide**: Fundamental execution hierarchy (Grid -> Thread Block -> Warp -> Thread).
- **PTX ISA & Memory Hierarchy**: Registers, Shared Memory (SRAM), L1/L2 caches, High Bandwidth Memory (HBM).
- **CUDA Synchronization & Streams**: Stream semantics, events, graphs (`cudaGraph_t`), and memory barriers.
- **Nsight Telemetry**: NVIDIA Nsight Systems (`nsys`) and Nsight Compute (`ncu`) metrics for memory bandwidth (% SOL HBM) and SM occupancy.

### PyTorch Systems Internals
- **Repository**: `https://github.com/pytorch/pytorch`
- **Key Modules**: `torch.cuda` memory allocator (caching allocator, block splitting), ATen tensor operations, Autograd engine, and PyTorch C++ dispatch architecture.

### Multi-GPU Collectives (NCCL)
- **Repository**: `https://github.com/NVIDIA/nccl`
- **Primitives**: `all-reduce` (ring, tree algorithms), `all-gather`, `reduce-scatter`, `broadcast`, point-to-point.
- **Interconnect Topologies**: NVLink / NVSwitch bandwidth vs. PCIe Gen4/Gen5 vs. InfiniBand / RoCE networks.

---

## 3. Foundational Research Papers

1. **PagedAttention & vLLM**:
   - Kwon et al., *"Efficient Memory Management for Large Language Model Serving with PagedAttention"*, SOSP 2023.
   - *Core Invariant*: Eliminates internal reservation waste and external fragmentation via OS-style virtual memory paging for KV caches.
2. **FlashAttention**:
   - Dao et al., *"FlashAttention: Fast and Memory-Efficient Exact Attention with IO-Awareness"*, NeurIPS 2022.
   - Dao, *"FlashAttention-2: Faster Attention with Better Parallelism and Work Partitioning"*, ICLR 2024.
   - *Core Invariant*: Tiling Q, K, V blocks in fast SRAM and computing online softmax eliminates O(N^2) memory transfers to HBM.
3. **Continuous Batching (Orca)**:
   - Yu et al., *"Orca: A Distributed Serving System for Transformer-Based Generative Models"*, OSDI 2022.
   - *Core Invariant*: Iteration-level scheduling allows newly arrived requests to join running batches and completed requests to depart immediately.
4. **Speculative Decoding**:
   - Leviathan et al., *"Fast Inference from Transformers via Speculative Decoding"*, ICML 2023.
   - Chen et al., *"Accelerating Large Language Model Decoding with Speculative Sampling"*, 2023.
   - *Core Invariant*: Verification of K speculative draft tokens in parallel costs approximately the same as a single-token autoregressive step.
5. **Chunked Prefill (Sarathi / vLLM V1)**:
   - Agrawal et al., *"Sarathi: Efficient LLM Inference by Piggybacking Decodes with Chunked Prefills"*, 2023.
   - *Core Invariant*: Breaking large prefill prompts into chunks co-scheduled with decode steps amortizes memory bandwidth overhead and stabilizes inter-token latency.
