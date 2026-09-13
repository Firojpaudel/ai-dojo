# vLLM Canonical Sources

## Primary Links
- **Repository**: https://github.com/vllm-project/vllm
- **Documentation**: https://docs.vllm.ai/
- **Design & RFCs**: Check `docs/source/design/` and RFC issue threads in the upstream repository.

## Operational Directives
1. Use the upstream repository to inspect the current production implementation.
2. Explicitly note the version tag (e.g. `v0.7.x` / `v1.0.x`) or commit hash checked.
3. Distinguish between vLLM V0 (original engine) and V1 (refactored high-performance engine architecture).
4. Use official unit and integration tests (`tests/`) as executable behavior specifications.
5. Use official benchmarks (`benchmarks/`) as empirical evidence for throughput and latency.
