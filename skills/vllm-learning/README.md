# AI Systems Apprenticeship — vLLM Learning Skill (v1.0.0)

A modular Agent Skill for learning modern AI inference systems deeply, using vLLM as the primary laboratory.

## Core Philosophy

> vLLM is the laboratory; AI systems mastery is the objective.

This skill enforces:
- **First-principles reasoning**: Derived from physical hardware constraints (memory bandwidth, compute intensity, PCIe/NVLink bottlenecks).
- **Primary-source-first research**: Current official source code, design RFCs, tests, and original papers over secondary summaries.
- **Interactive Socratic Q&A**: Concept Anchor -> Single Question -> Wait for learner response -> Evaluate mental model -> Minimal hints.
- **Evidence-based understanding**: Toy implementation from scratch, invariant tests, reproducible benchmarks, and upstream production code mapping.
- **Current-version awareness**: Explicit distinction between Research Papers, Legacy Architecture (v0), and Current Production Code (v1).
- **Strict Anti-Hallucination**: Grounding all technical assertions with explicit labels (`[VERIFIED]`, `[INFERRED]`, `[HYPOTHESIS]`, `[HISTORICAL]`, `[UNVERIFIED]`).

## Directory Structure

```text
vllm-learning/
├── SKILL.md                 # Main agent instructions and entry point
├── README.md                # Skill overview
├── session_commands.md      # Natural-language commands for learners
├── identity/                # Mentor role and learner profile
├── modes/                   # Specialized agent modes (teacher, socratic, debugger, etc.)
├── protocols/               # Rigorous execution protocols (Q&A, testing, benchmarking, etc.)
├── curriculum/              # 14-stage master curriculum roadmap
├── sources/                 # Canonical source registry and governance policies
├── templates/               # Reusable templates for lessons, benchmarks, and notes
└── state/                   # Progress, knowledge graph, and misconception tracking schemas
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
