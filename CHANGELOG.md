# Changelog

All notable changes to the skills in this repository will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [v2.2.0] - 2026-09-14

### Fixed
- **Phantom File References Purged**: Removed fabricated laboratory filenames (`block_allocator.py`, `test_block_allocator.py`, `benchmark_fragmentation.py`) in `curriculum/roadmap.md` Stage 05, keeping skills purely instructional without committing raw code stubs into the skill package.
- **Valid Relative Path Navigation**: Replaced nonexistent `./tests/test_block_table.py` with `./sources/SOURCE_REGISTRY.md` in `protocols/qa_session.md`.
- **NBLA Threshold Consistency**: Eliminated lingering float `< 0.60` thresholds in `protocols/lesson.md`, delegating dynamic Next-Best-Learning-Action selection directly to discrete levels `{0, 1, 2}` in `protocols/state_tracking.md` Section 4.
- **Host-Agnostic Tool Capabilities**: Reframed `[VERIFIED]` claim enforcement in `protocols/source_verification.md` and `SKILL.md` from IDE-specific tool identifiers to general capabilities (file-read, code-search, command-execution).
- **Shallow-Clone Compatible Architecture Mapping**: Updated `protocols/production_mapping.md` to reference V1 design RFCs/documentation rather than git history, preserving compatibility with `--depth 1` checkouts.
- **Malformed URI Corrected**: Replaced `file:///./` link with standard sibling-relative markdown link `[protocols/state_tracking.md](state_tracking.md)` in `protocols/lesson.md`.
- **Path Convention Unified**: Standardized path referencing in `protocols/qa_session.md` rule 5 to skill-root-relative (`curriculum/roadmap.md`) and document-relative paths, matching `SKILL.md`.
- **CI Dead-Reference Guard**: Added automated CI step in `.github/workflows/npx-skills.yml` verifying all referenced paths resolve and asserting zero malformed `file:///` URIs.

## [v2.1.0] - 2026-09-14

### Fixed
- **KV Cache Mathematical Correctness**: Fixed formula overcount in `curriculum/roadmap.md` to `2 * n_layers * n_kv_heads * d_head * seq_len * precision_bytes`, explicitly capturing Key & Value tensors and GQA/MQA memory reductions (e.g. 8× reduction on Llama-3-70B).
- **Physical Waste Bounding**: Replaced misleading "zero waste" claims with mathematically rigorous `<4% waste, strictly bounded to terminal block internal fragmentation: (block_size / 2) / seq_len`.
- **Tool-Bound `[VERIFIED]` Enforcement**: Prohibited emitting `[VERIFIED]` claim tags unless an active tool call in the session returned the primary-source evidence.

### Changed
- **Discrete 3-Level Competency Model**: Replaced unstable 2-decimal floats with observable discrete states `{0: None, 1: Scaffolded, 2: Autonomous}` in `protocols/state_tracking.md` and schema.
- **Standard Agent Skills Frontmatter**: Folded `use-when` trigger conditions directly into `description` in `SKILL.md` for native matching across Claude Code, Cursor, and Antigravity.
- **Repository Bootstrap Guidance**: Added explicit checkout bootstrap and commit-pinning directives in `protocols/production_mapping.md`.
- **Website Modernization**: Updated hero terminal to modern `vllm/v1/core/kv_cache_manager.py`, eliminated vaporware catalog cards, and unified all version references to `v2.1.0`.

## [v2.0.1] - 2026-09-14

### Changed
- **Dynamic Runtime Source Grounding**: Purged all deprecated vLLM V0 paths (`block_manager_v1.py`, `core/scheduler.py`) and invented line ranges; instituted the Dynamic Discovery Protocol via runtime grep and commit pinning against active vLLM V1 (`vllm/v1/...`).
- **Radical File Consolidation**: Pruned 43 redundant stub files (<300 bytes each) and consolidated curriculum, modes, sources, and templates into 25 high-density files; reduced `SKILL.md` size by 42%.
- **Canonical 14-Stage Roadmap**: Unified divergent stage outlines into one canonical source of truth (Stages 00–13) across `curriculum/roadmap.md`, `SKILL.md`, and `docs/index.html`.
- **Decoupled Workspace State**: Relocated learner progress persistence out of the package directory into `<workspace_root>/.vllm-learning/` so `npx skills add` updates never clobber learner history; eliminated drifting derived fields.
- **Host-Aware Turn Halting**: Provided universal question delivery (interactive UI modals when supported, clean chat blocks otherwise) with strict stop-and-wait turn halting across all agent runners.
- **LaTeX Cleanup & Website Modernization**: Removed all raw LaTeX delimiter leaks across markdown files; brought `docs/index.html` fully up to date with modern V1 scheduler tracing, complete 14-stage curriculum grid, and MIT licensing.

## [v2.0.0] - 2026-09-14

### Added
- **Adaptive 4-Block Learning Architecture**: Replaced rigid 22-step linear checklist with modular Core, Evidence, Production Mapping, and Mastery blocks driven by the Next-Best-Learning-Action (NBLA) engine.
- **Dynamic 12-Factor Competency Modeling**: Added `state/competencies.json` schema and `protocols/state_tracking.md` to continuously score and track multi-dimensional learner abilities.
- **Persistent Systems Misconception Tracking**: Added `state/misconceptions.json` for recording diagnosed mental models with ground-truth invariants and remediation gates.
- **Anti-Dependency & Scaffolding Fading**: Added Section 15 to `SKILL.md` and upgraded `protocols/implementation.md` with interface contracts, failing unit tests, and a 3-tier hinting ladder.
- **Hardware Fallback & Roofline Emulation**: Added Section 16 to `SKILL.md` and upgraded `protocols/benchmarking.md` for CPU tensor emulation and theoretical arithmetic intensity roofline derivations when NVIDIA GPUs are unavailable.
- **The 9-Level Abstraction Ladder**: Added Section 17 to `SKILL.md` and `protocols/abstraction_ladder.md` with explicit upshift and downshift operational directives.
- **Adversarial Defense & Fault Injection**: Added `protocols/adversarial_defense.md` and `templates/adversarial_challenge.md` covering injected defects, misleading benchmarks, and false optimization challenges.
- **Empirical Benchmarking Specification**: Upgraded `protocols/benchmarking.md` and `templates/experiment.md` with telemetry, locked GPU clocks, warmup iterations, synchronization, and latency distributions (p50/p90/p99).

### Changed
- **Zero-Hardcoding Guarantee**: Reset all state files to clean, unpolluted initial schemas; all paths evaluated and recorded by the agent are strictly relative.

## [v1.0.1] - 2026-09-14

### Changed
- **Interactive UI Modal Q&A**: Updated Section 11 and `protocols/qa_session.md` to trigger questions via the agentic `ask_question` tool with interactive options and write-in support, strictly halting execution until the learner replies.
- **Strict Single-Topic Mastery Gating**: Added Section 12 to prohibit generating scaffolding or tests for future stages until the current stage is verified, built, and explicitly approved by the learner.
- **Relative Repository Path Enforcement**: Added Section 13 requiring all file and code references to strictly use relative paths (`./level0_naive/...`) rather than absolute paths.
- **Chat Math Clean Formatting**: Added Section 14 requiring clean Unicode mathematical notation or monospace code blocks instead of raw LaTeX delimiters (`$...$`) in chat responses.
- **Curriculum State Initialization**: Initialized `state/progress.md` with active tracking for Level 0 (The Problem vLLM Solves).

## [v1.0.0] - 2026-09-13

### Added
- **`vllm-learning` Skill Release v1.0.0**:
  - Valid Agent Skills YAML frontmatter specification (`name: vllm-learning`).
  - Standardized repository layout under `skills/vllm-learning/` for discovery via `npx skills add`.
  - Interactive Socratic Q&A protocol (`protocols/qa_session.md`) enforcing the "One Question at a Time → Stop & Wait" turn pattern.
  - Stage mastery exam protocol (`protocols/mastery_exam.md`), teach-back protocol (`protocols/teach_back.md`), and adversarial oral defense protocol (`protocols/oral_defense.md`).
  - Strict source governance hierarchy and claim taxonomy (`[VERIFIED]`, `[INFERRED]`, `[HYPOTHESIS]`, `[HISTORICAL]`, `[UNVERIFIED]`) in `sources/SOURCE_POLICY.md` and `protocols/source_verification.md`.
  - Canonical source registries for vLLM, CUDA, PyTorch, NCCL, Transformers, and foundational research papers in `sources/`.
  - Current-version awareness protocol distinguishing Research Paper Architecture vs. Legacy (v0) vs. Current Production (v1).
  - Active source-to-source production mapping protocol (`protocols/production_mapping.md`).
  - Anti-drift topic classification (`CORE`, `SUPPORTING`, `OPTIONAL`, `DISTRACTION`) in `protocols/anti_drift.md`.
  - 14-stage AI systems curriculum roadmap covering Stage 0 (Foundations) to Stage 13 (Research).
