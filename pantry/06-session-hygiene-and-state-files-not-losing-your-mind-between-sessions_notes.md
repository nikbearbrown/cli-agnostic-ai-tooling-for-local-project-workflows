# Research Notes: Chapter 06 - Session Hygiene and State Files: Not Losing Your Mind Between Sessions

**Source:** TIKTOC.md chapter entry
**Notes file:** 06-session-hygiene-and-state-files-not-losing-your-mind-between-sessions_notes.md
**Corresponding chapter:** chapters/06-session-hygiene-and-state-files-not-losing-your-mind-between-sessions.md (not yet written)
**Generated:** 2026-06-14

---

## Chapter summary from TIKTOC.md

Context rot is behavioral as well as structural. Session hygiene and durable state files let readers start fresh without losing decisions.

---

## A. Conceptual foundations

### One task per session

The simplest session-hygiene rule is to keep sessions task-bounded. A session accumulates tool output, dead ends, and old assumptions. A fresh session with a good `status.md` can be higher quality than a long session with messy memory.

**Common misconception:** "A longer session is smarter because it knows more." It often knows more irrelevant material.

**Worked example:** Finish a chapter research task, write `session-handoff.md`, then start a new session for image generation rather than pivoting in the same context.

**Source(s):** Anthropic context engineering; Claude Code best practices.

### State lives outside the context window

`status.md` and `session-handoff.md` externalize current state. This makes context reset safe because decisions are stored in files, not only in chat history.

**Common misconception:** "The chat transcript is the project memory." It is expensive and hard to query. A short state file is cheaper and more reliable.

**Worked example:** `status.md` records current canonical chapter list, open questions, and next action. New agents read it instead of asking "what's going on?"

**Source(s):** Anthropic note-taking/agentic memory discussion; Claude Code memory docs.

### End-of-session ritual

The end-of-session update is the habit that keeps state files accurate. It should update status, handoff, manifest if canonical files changed, and output/archive locations.

**Common misconception:** "I will remember to summarize later." The summary is most accurate before ending the session.

**Worked example:** End a research session by writing "researched chapters 1-5; sources used; next research chapters 6-10; do not reread raw search pages."

**Source(s):** Anthropic context engineering on structured note-taking and compaction.

---

## B. Domain examples and cases

### Case 1: Book writing

A writer maintains `status.md` with current chapter drafted, researched, blocked, and ready for review. This prevents expensive reorientation every session.

### Case 2: Code migration

A migration task stores decisions and unresolved files in a handoff. The next session can continue without reading the whole conversation.

### Failure case: week-long thread

The agent contradicts itself because old decisions and newer decisions both remain in context. The fix is a state file plus fresh session.

---

## C. Connections and dependencies

**Prerequisites:**
- Chapter 5 accumulated context cost.

**Unlocks:**
- Chapter 7 compaction vs fresh-start decisions.
- Chapter 10 workflow patterns that use clean reviewer contexts.

**Adjacent chapter connections:**
- Chapter 5: identifies accumulated cost.
- Chapter 7: intervenes when accumulation has already happened.

---

## D. Current state of the field

**Settled:**
- Long-horizon agents need compaction, note-taking, or subagent architectures.
- External notes can preserve state with lower context overhead than full transcript.

**Contested or emerging:**
- Ideal schema for `status.md` is not standardized.
- Auto memory features vary by tool and can hide what was saved.

**Key references:**
1. Anthropic, "Effective context engineering for AI agents."
2. Claude Code memory docs.
3. Chroma, "Context Rot."

**Recent developments:**
- File-based memory and tool-native compaction are increasingly common, but portable state files remain the most tool-agnostic pattern.

---

## E. Teaching considerations

**Where students get stuck:**
- They write too much narrative in handoff files.
- They omit reasons for decisions, making future reversal likely.

**Analogies and framings that work:**
- `status.md` is the project dashboard; `session-handoff.md` is the shift-change note.

**Exercises:**
- Write a five-line status file for an active project.
- Restart a session using only handoff and measure what was lost.

---

## Local library cross-references

- `_lib_ai-claude-code-the-definitive-guide-to-agentic-development.md`
- `_lib_ai-nbb-prompt-architecture-the-power-of-the-template-pattern.md`

