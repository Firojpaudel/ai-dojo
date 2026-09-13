# Source Verification Protocol

## 1. Claim Classification Taxonomy

Every critical technical claim must be explicitly labeled with one of the following tags:

- **`[VERIFIED]`**: Confirmed by direct inspection of current source code, official documentation, or empirical test results with exact file/line/commit references.
- **`[INFERRED]`**: Logically derived from verified primitives, but not directly stated in a single primary source. The chain of deduction must be stated.
- **`[HYPOTHESIS]`**: An educated conjecture about system behavior requiring experimental or code inspection to validate.
- **`[HISTORICAL]`**: Accurate for earlier releases or original papers, but confirmed or suspected to diverge from current production implementation.
- **`[UNVERIFIED]`**: Stated in secondary sources or intuition, but not yet validated against primary source code or measurement.

## 2. Anti-Hallucination Rules

The agent must adhere strictly to these non-negotiable boundaries:
- **Never invent URLs**: If you do not know the exact URL, cite the repository/organization name and guide navigation.
- **Never invent source paths**: Do not guess file locations. Verify against the current repository tree.
- **Never invent function or class names**: Only reference symbols that exist in current or specified version code.
- **Never invent line numbers**: If exact lines cannot be verified, reference the containing class/function/method.
- **Never fabricate benchmark results**: Never quote throughput, latency, or memory numbers without specifying hardware, model, batch size, commit, and benchmark script.
- **Never claim to have inspected code or read a paper you have not checked**: State clearly: *"I could not verify this yet"* and inspect or search the canonical primary source.

## 3. Discovery vs. Evidence

- Search results, forum posts, blogs, and LLM summaries are **discovery tools**, NOT evidence.
- A claim becomes evidence only when traced back to:
  1. Current official source code
  2. Official documentation / design docs
  3. Official tests and benchmarks
  4. Original research papers
