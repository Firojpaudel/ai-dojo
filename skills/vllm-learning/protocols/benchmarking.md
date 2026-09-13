# Empirical Benchmarking & Profiling Protocol

## 1. Ground Truth Rule

Performance assertions without hardware metadata, workload distributions, warmup cycles, and variance metrics are anecdotes, not engineering evidence. Every benchmark must be reproducible and defensible.

## 2. Mandatory Experiment Specifications

When designing or evaluating a benchmark, require all components of this standard:

### A. Environment Telemetry
- **Hardware**: Exact GPU model, PCIe vs. SXM form-factor, Host CPU architecture, System RAM.
- **Clock Locks**: Locked GPU graphics/memory clocks (`nvidia-smi -lgc <clock>,<clock>`) to eliminate dynamic frequency scaling noise.
- **Driver & Runtime**: NVIDIA Driver version, CUDA Toolkit version, PyTorch version, and target git commit hash.

### B. Workload Definition
- **Model Specification**: Exact model architecture, parameter count, precision (`bfloat16`, `float8_e4m3fn`, `int4_awq`), and head configuration (MHA, GQA, MLA).
- **Request Distribution**: Arrival process (Poisson burst vs. fixed concurrency) and length distributions (e.g., prompt length $N_{in}$, generation length $N_{out}$).

### C. Measurement Rigor
- **Warmup Phase**: Minimum 10 warmup iterations discarded from calculation to stabilize JIT, CUDA graphs, memory pools, and caches.
- **Sample Size**: Minimum $N \ge 30$ iterations for statistical significance.
- **CUDA Stream Synchronization**: Mandatory `torch.cuda.synchronize()` before starting and stopping timers. Never time async CPU kernel launch overhead.
- **Cache Flushing**: When measuring cold kernel execution, clear device L2 cache (e.g., allocating and touching a dummy tensor equal to or larger than L2 cache size).

### D. Metric Distributions
- **TTFT (Time To First Token)**: Report p50, p90, p99 in milliseconds (ms).
- **TPOT (Time Per Output Token)**: Report p50, p90, p99 in milliseconds (ms).
- **Throughput**: Report both request throughput (req/s) and token generation throughput (tokens/s).
- **Memory Footprint**: Peak allocated VRAM, reserved VRAM, and KV cache utilization percentage.

## 3. Hardware Fallback: CPU & Virtual Roofline Mode

If the learner does not have access to an NVIDIA GPU:
1. **Never stall execution.**
2. **Execute CPU Simulation**: Run simplified PyTorch scripts on CPU with scaled-down dimensions.
3. **Derive Theoretical Roofline Metrics**:
   $$\text{Arithmetic Intensity } I = \frac{\text{Total FLOPs}}{\text{Total Memory Bytes Transferred}}$$
   $$\text{Attainable Performance } P = \min(\text{Peak Compute FLOP/s}, \, I \times \text{Peak Memory Bandwidth Byte/s})$$
4. Analyze memory traffic mathematically: calculate exactly how many bytes cross the memory bus for each decode step.
