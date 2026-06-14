# Research Notes: Chapter 05 - The Five Context Cost Types: Where Your Tokens Are Going

**Source:** TIKTOC.md chapter entry
**Notes file:** 05-the-five-context-cost-types-where-your-tokens-are-going_notes.md
**Corresponding chapter:** chapters/05-the-five-context-cost-types-where-your-tokens-are-going.md (not yet written)
**Generated:** 2026-06-14

---

## Chapter summary from TIKTOC.md

Before fixing an expensive session, readers need to identify which cost type is consuming context: fixed, per-task, accumulated, tool-output, or connector/MCP.

---

## A. Conceptual foundations

### Fixed cost

Fixed cost is everything loaded before the user's actual task: system prompt, always-loaded memory files, default rules, and tool schemas. It matters because a large fixed cost hurts every turn, not just one task.

**Common misconception:** "Only my prompt costs tokens." Tool schemas and memory files may already be in context.

**Worked example:** A session starts with system instructions, CLAUDE.md, path rules, and MCP tool schemas before the user asks the first question.

**Source(s):** Claude Code memory docs; Anthropic code execution with MCP.

### Per-task cost

Per-task cost is what the current task loads: file reads, search results, attachments, logs, command output. The fix is targeted retrieval, not global pruning.

**Common misconception:** "If it fits, load it." Long context can degrade even when it fits.

**Worked example:** Instead of reading a 20,000-line log, use `rg ERROR`, `tail`, or a parser and load only relevant excerpts.

**Source(s):** Anthropic effective context engineering.

### Accumulated cost

Accumulated cost is conversation history. It grows every turn. Compaction, handoff files, and fresh sessions are the main levers.

**Common misconception:** "Long sessions are efficient because they remember." They may remember too much, including dead ends and obsolete decisions.

**Worked example:** A four-hour debugging session contains wrong hypotheses that remain in context after the bug is fixed. A handoff file preserves the solution without the dead-end trace.

**Source(s):** Anthropic context engineering; Chroma context rot.

### Tool-output and connector/MCP cost

Tool output can linger in history after it has served its purpose. MCP schemas are fixed connector costs, while raw connector payloads are per-call costs. Anthropic's MCP/code execution article frames tool schema and intermediate payload handling as major efficiency problems.

**Common misconception:** "MCP cost happens only when I call the tool." Tool schemas can be visible to the model as part of available tool definitions even before a particular tool is used.

**Worked example:** A database MCP returns a huge JSON response; a better design computes the aggregate in the tool and returns only the result plus provenance.

**Source(s):** Anthropic, "Code execution with MCP," https://www.anthropic.com/engineering/code-execution-with-mcp

---

## B. Domain examples and cases

### Case 1: Bloated instruction file

A long CLAUDE.md or AGENTS.md repeats tutorials, examples, old decisions, and style notes. The fix is to keep core instructions short and move procedures to skills/workflows.

### Case 2: Raw JSON dump

A cloud API returns hundreds of fields, but the task needs three. Field filtering and pre-aggregation reduce context cost.

### Failure case: too many MCP servers

The user enables every available connector. Sessions slow down and degrade because the agent sees too many tool contracts and ambiguous tool choices.

---

## C. Connections and dependencies

**Prerequisites:**
- Chapter 1 context rot.

**Unlocks:**
- Chapter 6 session hygiene for accumulated cost.
- Chapter 7 compaction strategy.
- Chapter 9 MCP fixed cost.

**Adjacent chapter connections:**
- Chapter 4: instruction files can become fixed cost.
- Chapter 6: state files reduce accumulated cost.

---

## D. Current state of the field

**Settled:**
- Context is finite and should be curated.
- Long context and distractors degrade model reliability.
- Tool and connector design affects context efficiency.

**Contested or emerging:**
- Exact token overhead from MCP configurations varies by client and schema.
- Vendor-specific token accounting and compaction behavior changes quickly.

**Key references:**
1. Anthropic, "Effective context engineering for AI agents."
2. Anthropic, "Code execution with MCP."
3. Chroma, "Context Rot."
4. Claude Code memory docs.

**Recent developments:**
- Tool-search, code execution, and workflow engines are emerging to reduce schema/payload overhead.

---

## E. Teaching considerations

**Where students get stuck:**
- They want one fix for all token problems.
- They do not separate startup cost from task cost.

**Analogies and framings that work:**
- Context cost is rent, groceries, credit-card debt, and surprise fees. Each needs a different intervention.

**Exercises:**
- Ask readers to categorize every loaded item in a session into one of five cost types.
- Have them remove one fixed cost and one per-task cost, then compare behavior.

---

## Local library cross-references

- `_lib_ai-gigo-llm-toc.md`
- `_lib_ai-claude-code-the-definitive-guide-to-agentic-development.md`

