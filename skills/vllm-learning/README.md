# AI Systems Apprenticeship — vLLM Learning Skill (v2.0.1)

A modular Agent Skill for learning modern AI inference systems deeply, using vLLM as the primary laboratory.

## Core Philosophy

> vLLM is the laboratory; AI systems mastery is the objective.

This skill enforces:
- **First-principles reasoning**: Derived from physical hardware constraints (memory bandwidth, compute intensity, PCIe/NVLink bottlenecks).
- **Dynamic primary-source discovery**: Grounded in active checkouts via runtime grep and commit pinning over stale paths.
- **Turn-based single-question halting**: Host-aware questioning (interactive UI modals when supported, clean chat blocks otherwise) that strictly halts execution until the learner answers.
- **Anti-dependency scaffolding fading**: Interface stubs, failing unit tests, and a 3-tier calibrated hinting ladder.
- **Evidence-based understanding**: Toy implementation from scratch, invariant tests, reproducible benchmarks, and upstream production code mapping.
- **Decoupled workspace state**: Learner competency tracking persists in `<workspace_root>/.vllm-learning/`, safe from package updates.
- **Current-version awareness**: Explicit distinction between Research Papers, Legacy Architecture (v0), and Current Production Code (v1).
- **Strict Anti-Hallucination**: Grounding all technical assertions with explicit labels (`[VERIFIED]`, `[INFERRED]`, `[HYPOTHESIS]`, `[HISTORICAL]`, `[UNVERIFIED]`).

## Directory Structure

```text
vllm-learning/
├── SKILL.md                 # Main agent instructions and entry point
├── README.md                # Skill overview
├── session_commands.md      # Natural-language commands for learners
├── modes/                   # Mentor operational modes (modes/mentor_modes.md)
├── protocols/               # Rigorous execution protocols (Q&A, testing, benchmarking, etc.)
├── curriculum/              # 14-stage master curriculum roadmap (roadmap.md)
├── sources/                 # Canonical source registry and governance policies
├── templates/               # Reusable templates for experiments and adversarial challenges
└── state/                   # Competency and misconception tracking schemas
```

## Installation

Install using the Agent Skills CLI:

```bash
npx skills add Firojpaudel/ai-dojo --skill vllm-learning
```

Or install globally across agent environments:

```bash
npx skills add Firojpaudel/ai-dojo --skill vllm-learning -g
```
