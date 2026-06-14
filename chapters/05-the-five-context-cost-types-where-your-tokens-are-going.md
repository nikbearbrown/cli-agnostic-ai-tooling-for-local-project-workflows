# The Five Context Cost Types: Where Your Tokens Are Going

## Learning Objectives

By the end of this chapter, you should be able to:

- Name the five context cost types.
- Diagnose which cost type is dominating a session.
- Match each cost type to the right intervention.
- Audit one instruction or tool configuration for avoidable cost.

## Opening Case

You open a fresh agent session and ask a small question. It feels slow. The answer is worse than expected. You have not loaded a file yet, but the session is already heavy.

The hidden cost is startup context: instruction files, system prompts, and tool schemas. You are paying before you type.

## Core Concept

There are five context cost types:

| Cost type | What it is | Fix |
|---|---|---|
| Fixed | Always-loaded instructions, system prompt, tool schemas | Shorten rules; prune tools |
| Per-task | Files, searches, attachments for this task | Read targeted files |
| Accumulated | Conversation history | Compact, handoff, fresh session |
| Tool-output | Logs and command results | Summarize and trim |
| Connector/MCP | Tool schemas and returned payloads | Scope servers; aggregate in tools |

Anthropic frames context as a finite attention budget (https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents). Chroma's context-rot work shows reliability declines as long inputs accumulate distractors (https://www.trychroma.com/research/context-rot). Anthropic's MCP article explains why raw tool schemas and payloads can become substantial context overhead (https://www.anthropic.com/engineering/code-execution-with-mcp).

The key is that each cost type has a different fix. You do not solve a bloated `AGENTS.md` with compaction. You do not solve a week-long thread by deleting one MCP server.

One optimization cuts across tools that support prompt caching: keep stable material first and variable material last. Anthropic's prompt-caching documentation says caching depends on an identical prefix; the cache breaks when that prefix changes. So stable rules, examples, and templates belong before per-task details. Even when a tool does not expose caching, this ordering makes the prompt easier to reason about.

## Worked Example

A session starts badly. You audit it:

```text
Fixed:
  AGENTS.md: long
  CLAUDE.md: imports AGENTS.md plus extra duplicate rules
  MCP: GitHub, Slack, Drive, database all loaded

Per-task:
  Agent read entire docs/ folder

Accumulated:
  74 turns

Tool-output:
  900-line test log still in context
```

Fix order:

1. Trim duplicate rules.
2. Disable unrelated MCP servers.
3. Start a fresh session using `session-handoff.md`.
4. Replace full logs with failure excerpts.

**The lesson:** name the cost before choosing the cure.

**The limit:** most tools do not expose perfect token accounting, so use estimates and visible context breakdowns where available.

## Common Misconceptions

**Misconception: "All token problems are solved by compacting."**  
Compaction helps accumulated cost. It does not remove fixed startup cost.

**Misconception: "MCP cost happens only when I call the tool."**  
Tool schemas may be visible as part of the available tool surface before a call.

**Misconception: "Logs are harmless because they are text."**  
Logs are often high-volume, low-signal context.

## Token Audit Checklist

```text
Fixed:
[ ] Are always-loaded rules short?
[ ] Are all MCP servers needed for this task?

Per-task:
[ ] Did the agent read a whole folder?
[ ] Could search have narrowed the files first?

Accumulated:
[ ] Is this still one task?
[ ] Has the session crossed a natural handoff point?

Tool-output:
[ ] Are long logs summarized?
[ ] Is raw JSON filtered?

Ordering:
[ ] Are stable instructions before task-specific details?
[ ] Are examples reusable, or are they bloating every task?
```

## Exercises

1. Categorize the last 20 things loaded in an agent session.
2. Remove one fixed cost and one per-task cost.
3. Rewrite a log dump as a five-line diagnostic summary.

## What Would Change My Mind

I would revise the five-type model if tools exposed a better shared accounting model that divided context differently and proved more useful for intervention. Today, this model maps cleanly to the fixes practitioners can actually apply.

## Still Puzzling

- How much fixed context does each tool hide from the user?
- Will tool retrieval replace always-loaded schemas?
- What context budget threshold predicts visible quality drop in real work?
