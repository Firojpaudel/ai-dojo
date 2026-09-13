# Changelog

All notable changes to the skills in this repository will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

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
