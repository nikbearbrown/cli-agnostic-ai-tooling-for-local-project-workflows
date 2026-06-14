# Research Notes: Chapter 07 - Compaction, Clearing, and Knowing When to Start Fresh

**Source:** TIKTOC.md chapter entry
**Notes file:** 07-compaction-clearing-and-knowing-when-to-start-fresh_notes.md
**Corresponding chapter:** chapters/07-compaction-clearing-and-knowing-when-to-start-fresh.md (not yet written)
**Generated:** 2026-06-14

---

## Chapter summary from TIKTOC.md

Compaction, clearing, and fresh sessions are distinct interventions. The chapter teaches when to summarize and continue, reset after handoff, or start a new session.

---

## A. Conceptual foundations

### Compaction preserves continuity

Compaction summarizes the current session and continues with a compressed state. Anthropic describes compaction as preserving architecture decisions, unresolved bugs, and implementation details while discarding redundant outputs.

**Common misconception:** "Compaction is just deletion." Good compaction is selective preservation.

**Worked example:** Mid-feature coding task: compact with focus on accepted plan, files modified, tests failing, and next edit.

**Source(s):** Anthropic context engineering.

### Clearing removes history

Clearing is correct when switching tasks or when old context is actively harmful. It should be preceded by a handoff if continuity matters.

**Common misconception:** "Clear is a lighter compact." It is a reset, not a summary.

**Worked example:** After completing chapter research, write handoff, clear, then start image prompt work without carrying all research queries.

**Source(s):** Claude Code manage sessions docs should be checked before drafting for current command names.

### Fresh reviewer contexts

A fresh session is not only for saving tokens; it is a way to reduce confirmation bias. Reviewer agents should see the result, criteria, and diff, not the builder's whole reasoning trail.

**Common misconception:** "The reviewer needs all the history." Often the reviewer needs less history to be objective.

**Worked example:** Builder creates `pantry/` notes. Reviewer gets TIKTOC chapter spec, notes file, and quality checklist only.

**Source(s):** Anthropic context engineering on subagent architectures; Anthropic building effective agents.

---

## B. Domain examples and cases

### Case 1: Continuing a long code change

Use compaction if the task is the same and the history contains important state.

### Case 2: Switching from research to formatting

Use clear or fresh session because raw research path is not needed.

### Failure case: clearing without handoff

The user loses accepted decisions and reconstructs them from memory, introducing drift.

---

## C. Connections and dependencies

**Prerequisites:**
- Chapter 6 state files.

**Unlocks:**
- Chapter 10 clean reviewer/subagent patterns.
- Chapter 13 long-session failure modes.

**Adjacent chapter connections:**
- Chapter 6: prevention.
- Chapter 8: tool-specific commands vary, portable handoff remains.

---

## D. Current state of the field

**Settled:**
- Long-running agents need compaction or external note-taking.
- Tool commands differ; portable session handoff is stable.

**Contested or emerging:**
- Exact auto-compaction thresholds are vendor/version-specific and should not be overclaimed.
- Different tools preserve different artifacts after compaction.

**Key references:**
1. Anthropic, "Effective context engineering for AI agents."
2. Claude Code docs for current session commands.
3. Chroma context rot.

**Recent developments:**
- Tool-result clearing and more granular context editing are emerging as lighter alternatives to full compaction.

---

## E. Teaching considerations

**Where students get stuck:**
- They use `/clear` while still needing continuity.
- They compact without specifying what to preserve.

**Analogies and framings that work:**
- Compact is packing a suitcase; clear is leaving the room; fresh session is starting in a clean workshop.

**Exercises:**
- Given five session scenarios, choose compact, clear, or fresh session.
- Write a compaction focus prompt for a real active task.

---

## Local library cross-references

- `_lib_ai-claude-code-the-definitive-guide-to-agentic-development.md`

