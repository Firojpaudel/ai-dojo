# Source Verification Protocol

## 1. Claim Classification Taxonomy

Every critical technical claim must be explicitly labeled with one of the following tags:

- **`[VERIFIED]`**: Confirmed by direct inspection of current source code, official documentation, or empirical test results with exact file/commit references returned by an active tool call.
- **`[INFERRED]`**: Logically derived from verified primitives, but not directly stated in a single primary source. The chain of deduction must be stated.
- **`[HYPOTHESIS]`**: An educated conjecture about system behavior requiring experimental or code inspection to validate.
- **`[HISTORICAL]`**: Accurate for earlier releases or original papers, but confirmed or suspected to diverge from current production implementation.
- **`[UNVERIFIED]`**: Stated in secondary sources or parametric model memory, not yet validated against primary source code or measurement.

---

## 2. Mandatory Tool-Call Binding for `[VERIFIED]`

An agent is **strictly prohibited** from emitting the `[VERIFIED]` tag on any file path, class name, invariant, or benchmark metric unless an active tool call executing a verified inspection capability (such as file-read, code-search, or command-execution tools provided by the host environment, e.g., `view_file`/`ReadFile`, `grep_search`/`Grep`, `run_command`/`Bash`) executed in the session returned the primary source content cited.

If the agent has not executed a tool to inspect the primary source directly, it **must** label the statement `[INFERRED]` (if derived logically from physical principles) or `[UNVERIFIED]` (if relying on memory). Emitting `[VERIFIED]` without a supporting tool output is considered a severe anti-hallucination breach.

---

## 3. Anti-Hallucination Boundaries

The agent must adhere strictly to these non-negotiable boundaries:
- **Never invent URLs**: If you do not know the exact URL, cite the repository/organization name and guide navigation.
- **Never invent source paths**: Do not guess file locations. Grep the active repository tree.
- **Never invent function or class names**: Only reference symbols that exist in current or specified version code.
- **Never invent line numbers**: If exact lines cannot be verified, reference the containing class/function/method.
- **Never fabricate benchmark results**: Never quote throughput, latency, or memory numbers without specifying hardware, model, batch size, commit, and benchmark script.
- **Never claim to have inspected code you have not checked**: State clearly: *"I could not verify this yet"* and grep or inspect the primary source.

---

## 4. Discovery vs. Evidence

- Search results, forum posts, blogs, and LLM summaries are **discovery tools**, NOT evidence.
- A claim becomes evidence only when traced back to:
  1. Current official source code
  2. Official documentation / design docs
  3. Official tests and benchmarks
  4. Original research papers
