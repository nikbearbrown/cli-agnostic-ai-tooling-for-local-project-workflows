# Session Hygiene and State Files: Not Losing Your Mind Between Sessions

## Learning Objectives

By the end of this chapter, you should be able to:

- Explain why long sessions degrade even before the context window is full.
- Run a start/during/end session workflow.
- Write a useful `status.md`.
- Write a useful `session-handoff.md`.

## Opening Case

The first hour was sharp. The agent found the right files, made good edits, and remembered your constraints. Four hours later, it starts contradicting decisions you settled earlier. It revives a dead approach. It cites an old command.

The model did not become worse. The session became crowded.

## Core Concept

Session hygiene is the discipline of keeping the conversation narrow and moving durable state into files. Chroma's context-rot findings make the point bluntly: long context with distractors can degrade reliability (https://www.trychroma.com/research/context-rot). Anthropic's context-engineering guidance recommends managing what enters context and preserving useful state without carrying every intermediate token (https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents).

Use three files:

```text
_MANIFEST.md       tells what to read
status.md          tells current state
session-handoff.md tells the next session where to resume
```

The goal is not to make the agent remember everything. The goal is to make forgetting safe.

## Worked Example

End of a research session:

```markdown
# Session Handoff - CLI Tooling Book - 2026-06-14

## Goal
Draft chapter research notes from TIKTOC.md.

## Done
- Notes written for chapters 1-15 in pantry/.
- Eight local library files copied with _lib_ prefix.

## Next actions
1. Draft chapters from notes.
2. Keep citations inline.
3. Log word counts.

## Do not reload
- Raw web search results.
- Entire MD library.
```

The next session reads this file and starts clean.

**The lesson:** state files let you reset context without losing continuity.

**The limit:** a handoff is only as good as the decisions it records. If it omits the reason behind a choice, the next session may reverse it.

## Session Workflow

```text
Start:
1. Read _MANIFEST.md.
2. Read Tier 1 files.
3. Identify task domain.
4. Load only relevant Tier 2 files.
5. State a short plan.

During:
1. Keep tool output small.
2. Avoid unrelated pivots.
3. Record major decisions.

End:
1. Update status.md.
2. Write session-handoff.md.
3. Move superseded files to archive/.
4. Update _MANIFEST.md if canonical files changed.
```

## `status.md` Template

```markdown
---
project: project-alpha
status: active
updated: 2026-06-14
next:
  - draft chapter 4
  - verify Cursor rule docs
blocked_by: null
---

# Status

Current state, latest decisions, open questions, and next actions.
```

## Common Misconceptions

**Misconception: "The chat is the memory."**  
The chat is expensive memory. A state file is cheaper and easier to audit.

**Misconception: "Fresh sessions waste time."**  
Fresh sessions save time when the handoff is good.

**Misconception: "I should summarize everything."**  
No. Preserve decisions, current state, next actions, and relevant files.

## Exercises

1. Write `status.md` for one active project.
2. Write a handoff after your next session.
3. Start a fresh session using only the handoff and note what is missing.

## What Would Change My Mind

I would revise this chapter if agent tools developed transparent, accurate, portable long-term memory that preserved only useful decisions and reliably discarded noise. Current memory features are too tool-specific for that.

## Still Puzzling

- What is the ideal length for a handoff?
- Should session notes be archived by date automatically?
- Can agents reliably detect when a session should end?

