# Source Policy

## 1. Source Hierarchy

When making or verifying any technical claim about systems architecture, kernel behavior, or engine implementation, follow this strict descending hierarchy:

1. **Current Official Source Code**: Primary ground truth of software behavior.
2. **Current Official Documentation & Design RFCs**: Ground truth of intended architecture.
3. **Official Tests and Benchmarks**: Executable specifications and empirical evidence.
4. **Original Research Papers**: Theoretical foundation and initial algorithms.
5. **Official Maintainer Material**: Engineering blogs, core maintainer presentations, technical talks.
6. **Authoritative Ecosystem Documentation**: NVIDIA CUDA documentation, PyTorch docs, Linux kernel docs.
7. **High-Quality Secondary Sources**: Well-vetted engineering writeups, textbooks.
8. **Community Sources**: Forum discussions, StackOverflow, blog posts. (Allowed for discovery only, NEVER silent authority).

## 2. Discovery vs. Evidence

- **Discovery**: A web search, community article, or tutorial can point toward a potential file or solution.
- **Evidence**: You must inspect the underlying primary source (code, test, or documentation) before treating the claim as verified.
- Search results are **never** proof of current implementation behavior on their own.

## 3. Current-Version Awareness

Software evolves rapidly. Always distinguish:
- **Research Paper Architecture** (e.g., original PagedAttention paper)
- **Historical Implementation** (e.g., vLLM v0 architecture, legacy scheduler)
- **Current Production Implementation** (e.g., vLLM v1 engine architecture, chunked prefill, V1 async scheduling)

Whenever explaining implementation behavior, establish:
- **Project**: e.g., vLLM, PyTorch, FlashAttention
- **Branch/Version/Commit**: if relevant
- **Date Checked**: to ensure freshness
