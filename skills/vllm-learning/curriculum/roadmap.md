# Master Roadmap

## Stage 0 — Systems foundations
Linux, Python internals, processes/threads, networking, memory, profiling.

## Stage 1 — Deep learning execution
PyTorch tensors, autograd basics, modules, batching, device movement.

## Stage 2 — Transformer inference
Transformer architecture, attention, causal masking, logits, sampling, autoregressive generation.

## Stage 3 — Inference execution
Prefill, decode, KV cache, memory growth, latency, throughput.

## Stage 4 — Batching and scheduling
Static batching, padding, dynamic batching, continuous batching, token budgets, admission/scheduling.

## Stage 5 — KV memory systems
Allocation, fragmentation, blocks, logical/physical mapping, prefix caching, PagedAttention concepts.

## Stage 6 — GPU/CUDA
GPU architecture, memory hierarchy, kernels, synchronization, streams, graphs, profiling.

## Stage 7 — Attention and kernels
FlashAttention, memory traffic, tiling, fused kernels, kernel selection, numerical issues.

## Stage 8 — Inference engine architecture
API -> request state -> scheduler -> KV manager -> model runner -> sampler -> streaming.

## Stage 9 — vLLM source mastery
Current architecture, subsystem boundaries, call graphs, tests, benchmarks, configuration.

## Stage 10 — Distributed inference
Processes, NCCL, collectives, tensor/pipeline/data/expert parallelism, KV transfer.

## Stage 11 — Advanced serving
quantization, speculative decoding, prefix caching, chunked prefill, disaggregation, multimodal serving.

## Stage 12 — Performance engineering
profiling, bottleneck identification, workload design, regression analysis, capacity planning.

## Stage 13 — Research
literature review, hypotheses, experiment design, reproducibility, technical writing, open problems.

Progress through capability evidence, not calendar time.
