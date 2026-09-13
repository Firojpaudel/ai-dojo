# Empirical Benchmark & Experiment Record

## 1. Metadata
- **Experiment ID**: EXP-[ID]
- **Date**: YYYY-MM-DD
- **Target Mechanism**: [e.g. KV Cache Block Size vs. Memory Fragmentation]
- **Upstream Target Commit**: [commit hash / release tag]

## 2. Environment Telemetry
- **GPU Model & Form-Factor**: [e.g. NVIDIA A100-SXM4-80GB / CPU Fallback Mode]
- **GPU Clock State**: [e.g. Locked via nvidia-smi -lgc 1410,1215]
- **Driver & Runtime Versions**: NVIDIA Driver [X], CUDA [Y], PyTorch [Z]
- **Host System**: CPU [Model], RAM [Size GB], OS Kernel [Version]

## 3. Workload Configuration
- **Model Architecture & Precision**: [e.g. Llama-3-8B-Instruct, bfloat16]
- **Request Arrival Process**: [Poisson arrival rate / Fixed concurrency]
- **Prompt Length Distribution (N_in)**: [Fixed 1024 / Uniform(128, 2048)]
- **Generation Length Distribution (N_out)**: [Fixed 256 / Uniform(64, 512)]

## 4. Controlled Methodology
- **Warmup Iterations**: [>= 10]
- **Measured Iterations**: [>= 30]
- **Device Synchronization**: torch.cuda.synchronize() enforced before & after timers.
- **Cache State**: [L2 cache cleared between trials / Warm cache explicitly noted]

## 5. Empirical Results
| Workload / Config | TTFT p50 (ms) | TTFT p99 (ms) | TPOT p50 (ms) | TPOT p99 (ms) | Throughput (tok/s) | Peak VRAM (GB) |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: |
| Baseline | | | | | | |
| Variant A | | | | | | |
| Variant B | | | | | | |

## 6. Threats to Validity & Invariant Analysis
- Was thermal throttling detected?
- Did host CPU overhead saturate before GPU SMs reached saturation?
- What physical system invariant explains the difference in metrics?
