# Compaction, Clearing, and Knowing When to Start Fresh

## Learning Objectives

By the end of this chapter, you should be able to:

- Distinguish compaction, clearing, and fresh-session strategies.
- Choose the right intervention for a degraded session.
- Write a focused compaction prompt.
- Preserve continuity before clearing context.

## Opening Case

You are halfway through a migration. The session is getting sluggish, so you type the reset command. The tool clears the context. Now the agent no longer knows the accepted plan, the files already touched, or the test failure you were chasing.

The problem was real. The intervention was wrong.

## Core Concept

Compaction, clearing, and starting fresh solve different problems.

**Compaction** summarizes and continues. Use it when the same task is ongoing and the history contains decisions worth preserving.

**Clearing** resets. Use it when the previous task is done or actively misleading.

**Fresh session** starts with clean context, usually from `session-handoff.md`. Use it for unrelated tasks or independent review.

Anthropic's context-engineering guidance describes compaction as a way to retain decisions while reducing redundant history. The important portable rule is not the command name. The portable rule is: decide what state must survive before you reset.

## Worked Example

Bad compaction request:

```text
/compact
```

Better:

```text
/compact Keep only: accepted plan, files changed, unresolved test failure,
current assumptions, and next two actions. Drop dead-end debugging paths.
```

Fresh session handoff:

```text
Read session-handoff.md, _MANIFEST.md, and PROJECT_RULES.md.
Do not read raw logs unless the failing test still reproduces.
```

**The lesson:** compaction is not magic. It is only as good as the focus you provide.

**The limit:** tool-specific compaction behavior changes. Treat command tables as "last verified" material, not eternal truth.

## Decision Rule

```text
Use compaction when:
- Same task continues.
- History contains useful decisions.
- You can name what to keep.

Use clear when:
- Task is done.
- Context is misleading.
- Handoff has been written if continuity matters.

Use fresh session when:
- Task domain changes.
- You need an unbiased reviewer.
- Session has accumulated many dead ends.
```

## Common Misconceptions

**Misconception: "Compact and clear are interchangeable."**  
Compact preserves selected state. Clear removes history.

**Misconception: "Auto-compaction means I do not need session hygiene."**  
Auto-compaction is a fallback, not a workflow.

**Misconception: "Reviewers need full history."**  
Reviewers often need the diff, rules, and acceptance criteria, not the builder's whole trail.

## Exercises

1. Write a compaction focus prompt for a current task.
2. Take one old session and decide whether it should have been compacted, cleared, or handed off.
3. Create a reviewer prompt that excludes builder history.

## What Would Change My Mind

I would revise this chapter if tools exposed reliable, inspectable compaction summaries with clear guarantees about what was preserved. Current compaction remains partly opaque and tool-specific.

## Still Puzzling

- What should auto-compaction preserve by default?
- Should tools show a diff of context removed?
- Can reviewers be too context-starved?

