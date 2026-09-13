# Changelog

All notable changes to the skills in this repository will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

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
