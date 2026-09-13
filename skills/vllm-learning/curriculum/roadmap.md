# Master Curriculum Roadmap — AI Inference Systems (Stages 00–13)

A rigorous, evidence-driven 14-stage curriculum for mastering modern AI inference systems from hardware first principles to production engine internals.

Progress is governed strictly by **capability evidence and physical invariant verification**, never calendar time.

---

## Stage 00 — Systems Foundations
- **Core Topics**: Linux systems programming, process vs. thread execution models, memory hierarchies (registers, L1/L2/L3 caches, DRAM), virtual memory, page tables, OS page faults, I/O multiplexing, and basic profiling (perf, strace).
- **Physical Invariants**: DRAM access latency (~50-100 ns) vs. L1 cache (~1 ns); memory bandwidth saturation; page table walking overhead.
- **Milestone Deliverable**: Written analysis and benchmark of CPU memory access patterns demonstrating cache-line bouncing and TLB miss penalties.

---

## Stage 01 — Deep Learning Execution & Tensors
- **Core Topics**: PyTorch execution internals, tensor memory layouts (strides, contiguous vs. non-contiguous storage), device memory allocation (torch.cuda), compute graphs, forward vs. backward execution overhead, and CPU-GPU device transfer bottlenecks.
- **Physical Invariants**: PCIe transfer bandwidth (e.g., PCIe Gen4 x16 ~31.5 GB/s) vs. GPU HBM bandwidth (e.g., A100 ~2 TB/s). Transferring tensors over PCIe stalls GPU execution.
- **Milestone Deliverable**: Standalone script benchmarking Host-to-Device vs. Device-to-Host transfer latency across varied batch and hidden dimensions, isolating pinned memory effects.

---

## Stage 02 — Transformer Inference Mechanics
- **Core Topics**: Autoregressive decoding loop, causal masking, Multi-Head Attention (MHA), Multi-Query Attention (MQA), Grouped-Query Attention (GQA), token projection FLOPs, logit computation, and sampling strategies (temperature, top-p, top-k).
- **Physical Invariants**: Matrix multiplication arithmetic intensity during single-token generation vs. prompt ingestion. 
- **Milestone Deliverable**: Minimal standalone transformer generation loop written from scratch without high-level library abstractions, measuring per-token execution times.

---

## Stage 03 — Prefill vs. Decode & The KV Cache Bottleneck
- **Core Topics**: The fundamental asymmetry of LLM inference: compute-bound prefill phase vs. memory-bandwidth-bound decode phase. The quadratic compute of attention (O(N²) prompt) vs. linear token-by-token generation. Exact KV cache footprint equation: `2 * n_layers * n_kv_heads * d_head * seq_len * precision_bytes` (where the initial factor of 2 accounts for Key and Value tensors, and `n_kv_heads` captures MHA, MQA where `n_kv_heads = 1`, and GQA where `n_kv_heads < n_heads`). Derive how GQA reduces KV cache memory footprint by 4–8x compared to MHA (e.g. Llama-3-70B: 64 query heads vs. 8 KV heads).
- **Physical Invariants**: Arithmetic Intensity I = FLOPs / Bytes. Why decode arithmetic intensity is typically <= 1 FLOP/Byte, fundamentally bottlenecked by GPU HBM memory bandwidth.
- **Milestone Deliverable**: Toy generative model comparing memory traffic with and without KV caching, verifying that without cache, computation scales quadratically per generated token.

---

## Stage 04 — Continuous Batching & Iteration Scheduling
- **Core Topics**: Static batching and padding inefficiency; cellular batching; iteration-level (continuous) batching (Orca architecture). Scheduler states: WAITING, RUNNING, SWAPPED. Dynamic preemption policies, recomputation vs. swap trade-offs, and token budget allocation.
- **Physical Invariants**: Under static batching, short sequences hold GPU memory idle while waiting for the longest sequence in the batch, causing severe throughput collapse.
- **Milestone Deliverable**: Python implementation of a continuous batching iteration-level scheduler handling dynamic arrivals, early departures, and preemption under memory limits.

---

## Stage 05 — Paged KV Memory Systems & PagedAttention
- **Core Topics**: The physical memory fragmentation problem: internal reservation waste (pre-allocating for max_seq_len) and external fragmentation (varying request lifetimes). Operating system virtual memory paging analogy. Logical-to-physical block tables, fixed-size KV blocks, non-contiguous physical allocation, copy-on-write (CoW) for parallel sampling, and prefix caching. Mathematical derivation of terminal block internal waste: `average waste = (block_size / 2) / seq_len` (< 4% for block_size=16 and seq_len >= 256).
- **Physical Invariants**: Memory waste is bounded strictly to the final block of each sequence (< 4% overall waste), completely eliminating external fragmentation and upfront reservation waste.
- **Milestone Deliverable**: Implement a paged block allocator with logical-to-physical block mapping, copy-on-write fork mechanics, and a fragmentation simulator verifying < 4% terminal waste on synthetic workloads.

---

## Stage 06 — GPU Architecture & CUDA Execution Dynamics
- **Core Topics**: NVIDIA GPU hardware architecture: Streaming Multiprocessors (SMs), Warp Schedulers, Tensor Cores, Shared Memory, L1/L2 caches, and High Bandwidth Memory (HBM). Warp divergence, memory coalescing, bank conflicts in shared memory, CUDA streams, CUDA event synchronization, and CUDA execution graphs.
- **Physical Invariants**: 32 threads in a warp execute in lockstep; uncoalesced global memory loads trigger multiple 32-byte cache line transactions, reducing effective bandwidth.
- **Milestone Deliverable**: Benchmark demonstrating memory coalescing vs. strided memory access degradation using PyTorch CUDA custom operations or Triton, instrumenting memory throughput.

---

## Stage 07 — Attention Kernels & Memory Traffic
- **Core Topics**: Standard attention memory IO bottleneck (writing intermediate N x N attention matrix to HBM). FlashAttention-1/2/3 principles: online softmax, tiling across SRAM, fusing operations, and avoiding HBM read/write of attention weights. IO-aware algorithmic complexity.
- **Physical Invariants**: SRAM access is orders of magnitude faster (~19 TB/s aggregate) than HBM (~2 TB/s). Minimizing HBM roundtrips yields 2-4x end-to-end speedups even when total FLOPs increase slightly.
- **Milestone Deliverable**: Analytical derivation and numerical verification of online softmax scaling, showing mathematical equivalence to standard two-pass softmax.

---

## Stage 08 — Inference Engine Architecture
- **Core Topics**: Anatomy of a production LLM serving runtime: client ingress/API handling, asynchronous request pipeline, engine execution loop, tokenizer/detokenizer threads, model runner abstractions, GPU memory profiling during initialization, and token streaming mechanics.
- **Physical Invariants**: Decoupling the asyncio web/scheduler thread from the GPU worker execution thread to prevent event-loop latency jitter from starving GPU execution queues.
- **Milestone Deliverable**: Architectural blueprint and minimal mock engine executing asynchronous requests through a decoupled scheduler and worker loop.

---

## Stage 09 — vLLM Production Source Mastery
- **Core Topics**: Upstream production architecture of vLLM. Transition from legacy V0 to modern V1 architecture: multiprocessing core, chunked prefill by default, unified block manager, model runner execution flow, and upstream test harnesses.
- **Physical Invariants**: Tracing execution from request arrival through the V1 scheduler directly down to model runner execution without relying on deprecated V0 paths.
- **Milestone Deliverable**: End-to-end source code trace identifying the exact classes, invariants, and data flow in the current upstream vLLM repository for a single forward pass.

---

## Stage 10 — Distributed Inference & Collectives
- **Core Topics**: Multi-GPU scaling: Tensor Parallelism (Megatron-LM style row/column parallel linear layers), Pipeline Parallelism, Data Parallelism, and Expert Parallelism (MoE routing). NCCL communication primitives (all-reduce, all-gather, reduce-scatter, p2p). Communication vs. computation overlap.
- **Physical Invariants**: NVLink bandwidth (e.g. 600–900 GB/s) vs. inter-node InfiniBand (e.g. 50–100 GB/s). All-reduce communication overhead increases with world size and bounds small-batch latency.
- **Milestone Deliverable**: Mathematical and architectural breakdown of Tensor Parallelism for an MHA/MLP block, calculating exact communication bytes per token generated.

---

## Stage 11 — Advanced Serving & Optimization
- **Core Topics**: Chunked prefill (co-scheduling prefill chunks with decode steps to eliminate TTFT/ITL trade-offs), speculative decoding (draft model verification, tree attention, rejection sampling), disaggregated prefill and decode (separate hardware clusters with KV transfer), weight quantization (FP8, AWQ, GPTQ, INT4), and KV cache quantization.
- **Physical Invariants**: Speculative decoding trade-off: speedup is strictly bounded by target verification time and draft model acceptance rate alpha.
- **Milestone Deliverable**: Speculative decoding simulation demonstrating acceptance rate dynamics and verifying exact mathematical bounds on expected tokens per step.

---

## Stage 12 — Performance Profiling & Bottleneck Isolation
- **Core Topics**: Systems profiling using NVIDIA Nsight Systems (nsys) and Nsight Compute (ncu). Interpreting GPU traces: kernel launch delays, CPU synchronization stalls, memory bandwidth utilization (% SOL HBM), and SM compute utilization (% SOL SM). Roofline analysis: calculating whether a workload is memory or compute bound. Tail latency distributions (p50, p90, p99, p99.9).
- **Physical Invariants**: Identifying whether latency spikes are caused by CUDA runtime synchronization, memory allocation, or host CPU thread contention.
- **Milestone Deliverable**: Empirical profile report with annotated timeline isolating a simulated or real bottleneck and prescribing architectural fixes.

---

## Stage 13 — Systems Research & Empirical Discovery
- **Core Topics**: Formulating verifiable systems hypotheses, designing controlled experiments with statistical rigor, identifying threats to validity, evaluating novel inference algorithms from recent literature, and contributing upstream RFCs.
- **Physical Invariants**: Reproducibility requires locked GPU clocks, strict warmup phases, explicit cache invalidation, and complete hardware telemetry reporting.
- **Milestone Deliverable**: Publication-grade technical research note containing a formalized hypothesis, experimental data, roofline analysis, and architectural conclusions.
