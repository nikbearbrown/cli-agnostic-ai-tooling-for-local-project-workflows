# Research Notes: Chapter 13 - The Failure-Mode Catalog: Root Causes and Mitigations

**Source:** TIKTOC.md chapter entry
**Notes file:** 13-the-failure-mode-catalog-root-causes-and-mitigations_notes.md
**Corresponding chapter:** chapters/13-the-failure-mode-catalog-root-causes-and-mitigations.md (not yet written)
**Generated:** 2026-06-14

---

## Chapter summary from TIKTOC.md

The failure-mode catalog maps patterns to triggers and mitigations: manifest discipline failures, ignore-file limits, adapter duplication, memory index overflow, stale status, bad handoffs, long sessions, over-reporting reviewers, and unverifiable vendor figures.

---

## A. Conceptual foundations

### Failure mode = pattern + trigger + mitigation

The reader needs more than a symptom list. Each failure should be framed as: what pattern failed, under what trigger, and which mitigation fits.

**Common misconception:** "The same symptom always has the same cause." A wrong answer can come from stale status, old files, over-broad context, or tool-specific instruction failure.

**Worked example:** Agent reads archive despite manifest. Trigger may be vague prompt, lack of ignore enforcement, or a broad grep/search task.

**Source(s):** Synthesized from previous chapter sources.

### Ignore files are not security

Ignore mechanisms are useful for reducing context and git noise, but secrets should not be in project folders. Many tools have best-effort or tool-specific ignore behavior.

**Common misconception:** ".gitignore means the agent cannot see it." Git ignore controls git tracking, not necessarily tool read access.

**Worked example:** `.env` ignored by git but still present on disk. Agent with filesystem access may read it if not otherwise blocked.

**Source(s):** Git ignore docs; Claude memory/security docs; prompt injection/security literature.

### Stale indexes and stale state

Any index (`_MANIFEST.md`, `status.md`, memory files) can become wrong. The catalog should teach mitigation through update rituals and validation checks.

**Common misconception:** "Indexes are always net positive." A stale index can be worse than no index.

**Worked example:** `status.md` says Chapter 3 is drafted; actual chapters directory has only placeholder files. Future agents plan from false state.

**Source(s):** Anthropic context engineering on stale indexing and just-in-time retrieval.

---

## B. Domain examples and cases

### Case 1: Manifest ignored

The user asks "summarize everything." The agent reads Tier 3. Mitigation: better prompt, physical archive separation, and/or ignore file.

### Case 2: Duplicated AGENTS import

Tool reads both `AGENTS.md` and an importing adapter, duplicating context. Mitigation: test startup context; use compile strategy when needed.

### Failure case: measurement built on vendor numbers

The reader designs around "99%" token reduction from one report. The fix is local measurement and labels.

---

## C. Connections and dependencies

**Prerequisites:**
- Chapters 5-11.

**Unlocks:**
- Chapter 14 governance analysis.
- Chapter 15 empirical measurement.

**Adjacent chapter connections:**
- Chapter 12: checklist symptoms.
- Chapter 14: security-related failure modes.

---

## D. Current state of the field

**Settled:**
- Long context, stale context, and distractors can degrade reliability.
- Tool behavior differs; portable conventions need verification.

**Contested or emerging:**
- Exact reliability of manifest discipline across tools is not well quantified.
- Ignore-file semantics vary and may not be reliable enough for secrets.

**Key references:**
1. Chroma context rot.
2. Anthropic context engineering.
3. ABTest behavior-driven testing for coding agents, arXiv 2604.03362.
4. Git ignore docs.

**Recent developments:**
- Behavior-driven fuzzing and empirical studies are beginning to replace anecdotal failure catalogs.

---

## E. Teaching considerations

**Where students get stuck:**
- They jump to fixes without identifying triggers.
- They overgeneralize one tool's behavior.

**Analogies and framings that work:**
- Failure diagnosis is like debugging: symptom, reproduction, root cause, minimal fix.

**Exercises:**
- For three recent failures, fill a table: symptom, pattern, trigger, mitigation, prevention.
- Rewrite a vague failure report into a testable reproduction.

---

## Local library cross-references

- `_lib_ai-gigo-llm-toc.md`
- `_lib_ai-claude-code-the-definitive-guide-to-agentic-development.md`

