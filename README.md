# ai-dojo

A curated repository of production-grade Agent Skills designed for deep engineering apprenticeships.

## Overview

Modern AI inference engineering requires understanding systems from first principles: memory bandwidth hierarchies, kernel execution dynamics, distributed communication collectives, and scheduler invariants. `ai-dojo` provides agent skills that guide learners through hands-on systems investigation rather than passive summary generation.

## Available Skills

### `vllm-learning`

A comprehensive AI-systems apprenticeship for learning modern inference engines from first principles, using vLLM as the primary laboratory.

- **Directory**: [`skills/vllm-learning/`](skills/vllm-learning/)
- **Entry Point**: [`skills/vllm-learning/SKILL.md`](skills/vllm-learning/SKILL.md)
- **Specification Version**: 2.2.0
- **Key Capabilities**:
  - **Adaptive 4-Block Learning Architecture**: Modular Core, Evidence, Production Mapping, and Mastery blocks driven dynamically by the Next-Best-Learning-Action (NBLA) engine.
  - **Dynamic 12-Factor Competency Modeling**: Real-time continuous scoring across intuition, math, code, testing, benchmarking, profiling, and production tracing.
  - **Persistent Systems Misconception Tracking**: Explicit diagnosis, logging, and remediation gating for systems fallacies.
  - **Anti-Dependency & Scaffolding Fading**: Enforces interface contracts, failing unit tests, and a 3-tier hinting ladder to maximize learner autonomy.
  - **Turn-Based Single-Question Halting**: Host-aware questioning (interactive UI modals when supported, clean chat blocks otherwise) that strictly halts execution until the learner answers.
  - **Strict Source Governance**: Prioritizes current source code, official documentation, executable tests, and primary research papers over secondary summaries.
  - **Anti-Hallucination Tagging**: Formally categorizes all technical claims (`[VERIFIED]`, `[INFERRED]`, `[HYPOTHESIS]`, `[HISTORICAL]`, `[UNVERIFIED]`).
  - **Dynamic Production Source Grounding**: Discovers upstream entry points in active checkouts via runtime grep and commit pinning, eliminating stale paths.
  - **Decoupled Workspace State**: Persists learner progress in `<workspace_root>/.vllm-learning/`, safe from package reinstallation.
  - **Hardware Fallback & Roofline Mode**: CPU tensor emulation and theoretical arithmetic intensity roofline derivations when NVIDIA GPUs are unavailable.

---

## Installation via Agent Skills CLI

Install directly into your local project environment:

```bash
npx skills add Firojpaudel/ai-dojo --skill vllm-learning
```

Install globally across all supported agent environments (Claude Code, Cursor, Copilot, Antigravity):

```bash
npx skills add Firojpaudel/ai-dojo --skill vllm-learning -g
```

To list all available skills in this repository:

```bash
npx skills add Firojpaudel/ai-dojo --list
```

---

## Repository Architecture

```text
ai-dojo/
├── README.md
├── CHANGELOG.md
├── .gitignore
└── skills/
    └── vllm-learning/
        ├── SKILL.md                 # Agent Skill definition (YAML frontmatter + instructions)
        ├── README.md                # Skill documentation
        ├── session_commands.md      # Natural-language commands
        ├── identity/                # Mentor role and learner profile guidelines
        ├── modes/                   # Teacher, Socratic, Debugger, Benchmarker, etc.
        ├── protocols/               # Q&A, Testing, Benchmarking, Source Verification, Anti-Drift
        ├── curriculum/              # 14-stage roadmap and subject deep dives
        ├── sources/                 # Canonical registries (vLLM, CUDA, PyTorch, NCCL, Papers)
        ├── templates/               # Lesson, experiment, benchmark, and note templates
        └── state/                   # State tracking schemas
```

---

## License

MIT
