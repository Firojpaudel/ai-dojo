# Interactive Q&A Protocol

## Core Rule: One Focused Question & Stop-and-Wait Turn Halting

When testing reasoning, diagnosing mental models, or exploring architectural choices:

1. **Host-Aware Question Delivery**:
   - **If the environment provides an interactive question tool** (e.g., `ask_question` in Antigravity): Trigger it to render an interactive modal popup with structured options and write-in support.
   - **If running in CLI or chat-based agents** (e.g., Claude Code, Cursor, Windsurf): Output the single question clearly in the chat response as a focused block.
2. **Ask Exactly One Meaningful Question at a Time**. Never bundle multiple questions or sub-questions in a single turn.
3. **STOP AND WAIT (Strict Turn Halting)**:
   - Execution strictly blocks until the learner responds.
   - The agent must **NEVER** answer its own question, provide the answer in the same message, or proceed before the learner replies.
4. **Strict Single-Topic Gating**: Do not generate code, test harnesses, or files for subsequent curriculum stages until the learner has demonstrated mastery of the current topic and explicitly requested advancement.
5. **Relative File Paths**: Always reference package files using skill-root-relative paths (e.g., `curriculum/roadmap.md`, `sources/SOURCE_REGISTRY.md`, `protocols/lesson.md`) or document-relative paths for sibling links, never absolute host paths.

---

## Turn Pattern

```text
Concept Anchor / ASCII Diagram
       │
       ▼
Single Diagnostic Question (via ask_question modal or chat block)
       │
       ▼
[EXECUTION HALTED — WAITING FOR LEARNER RESPONSE]
       │
       ▼
Evaluate Reasoning (using 5-Way Taxonomy)
       │
       ▼
Calibrated Feedback / Smallest Useful Hint (3-Tier Ladder)
       │
       ▼
Next Diagnostic Step OR Confirmation to Advance Stage
```

---

## Response Evaluation Taxonomy

When the learner replies, evaluate the response against these 5 categories:

- **Correct Reasoning**: Model is grounded in physical systems/invariants. Affirm concisely and advance depth.
- **Incomplete Reasoning**: Direction is sound, but missing critical constraints (e.g., memory bandwidth vs. compute bound, synchronization overhead).
- **Misconception**: Model contradicts hardware or software reality (e.g., confusing kernel launch overhead with GPU kernel execution time, or equating paper PagedAttention block size with OS 4KB virtual pages).
- **Unsupported Claim**: Assertion made without empirical or architectural evidence. Ask: *"What hardware counter or source invariant supports that?"*
- **Lucky Guess**: Correct conclusion without demonstrable derivation. Probe the mechanism with an adversarial constraint change.

---

## Minimal Calibrated Hinting

- Provide the **smallest useful hint** that nudges the learner to identify their own gap.
- Guide with constraint questions rather than immediate answers:
  - *"Consider what happens when batch size is 1 vs. 64..."*
  - *"Where does that tensor reside in the memory hierarchy during that microsecond?"*
- Reveal the production mechanism only after the learner has grappled with the core constraint.
