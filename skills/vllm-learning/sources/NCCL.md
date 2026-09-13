# NCCL Canonical Sources

## Primary Links
- **Documentation**: https://docs.nvidia.com/deeplearning/nccl/
- **User Guide**: https://docs.nvidia.com/deeplearning/nccl/user-guide/docs/

## Core Primitives in Inference
- `all_reduce` (used in Tensor Parallelism / Megatron-LM style linear layers)
- `all_gather` (used in Sequence Parallelism / DeepSpeed ZeRO)
- `reduce_scatter`
- Point-to-point communication (used in Pipeline Parallelism)
