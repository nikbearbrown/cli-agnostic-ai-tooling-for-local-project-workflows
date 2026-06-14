# Research Notes: Chapter 12 - The Anti-Patterns Checklist: Eleven Things You're Probably Still Doing

**Source:** TIKTOC.md chapter entry
**Notes file:** 12-the-anti-patterns-checklist-eleven-things-youre-probably-still-doing_notes.md
**Corresponding chapter:** chapters/12-the-anti-patterns-checklist-eleven-things-youre-probably-still-doing.md (not yet written)
**Generated:** 2026-06-14

---

## Chapter summary from TIKTOC.md

A fast audit checklist of eleven structural and behavioral anti-patterns: giant parent folders, mixed projects, old drafts beside current drafts, outputs as source, huge global memory, unrelated tasks in one session, full logs/JSON dumps, no status file, vague tasks, unreviewed delete/rename, and tool-specific dependency.

---

## A. Conceptual foundations

### Anti-patterns are symptoms of weak boundaries

Most anti-patterns reduce to unclear boundaries: project boundaries, source/output boundaries, current/archive boundaries, session boundaries, or tool-portability boundaries.

**Common misconception:** "These are separate little mistakes." They are recurring manifestations of the same context-boundary problem.

**Worked example:** Old drafts beside current drafts and outputs becoming source are both failures to mark canonical status.

**Source(s):** Anthropic context engineering; Chroma context rot.

### Prioritization matters

The checklist should not imply all fixes have equal value. High-impact fixes: bounded project root, archive separation, short rules file, status file, no-delete gate.

**Common misconception:** "I need to fix all eleven before working." Start with the anti-pattern causing current failures.

**Worked example:** If sessions degrade, fix session/task boundaries before adding more project adapters.

**Source(s):** Practitioner synthesis from previous chapters.

### Checklists teach transfer

The checklist chapter should function as a self-audit the reader can run without remembering every conceptual chapter. It is the most "reference handbook" part of the book.

**Common misconception:** "A checklist is shallow." For operational work, a checklist is the way concepts become behavior.

**Worked example:** 15-minute audit: list root folders, find old/current mixing, inspect instruction file length, identify generated outputs.

**Source(s):** Atul Gawande checklist literature could be optional background; primary book sources are previous chapter sources.

---

## B. Domain examples and cases

### Case 1: Six anti-patterns in a book repo

Flat drafts, old exports, no manifest, long session, no handoff, vague "clean up" prompt. Fix order: manifest, archive, status, session reset.

### Case 2: Three anti-patterns in code repo

Generated clients edited by agent, huge global rules, no test-before-write. Fix: mark generated as Tier 3, split path rules, add tests.

### Failure case: audit without action

The reader checks boxes but does not choose top three fixes. Chapter should force prioritization.

---

## C. Connections and dependencies

**Prerequisites:**
- Chapters 1-11 provide the explanation behind each checklist item.

**Unlocks:**
- Chapter 13 deeper failure-mode diagnosis.
- Chapter 15 measurement of fixes.

**Adjacent chapter connections:**
- Chapter 11: file safety anti-patterns.
- Chapter 13: root cause catalog.

---

## D. Current state of the field

**Settled:**
- Common agent workflow failures cluster around context pollution, stale state, broad reads, and weak safety gates.

**Contested or emerging:**
- Anti-pattern lists are practitioner-synthesized, not formal standards.

**Key references:**
1. Anthropic context engineering.
2. Chroma context rot.
3. Claude memory docs for instruction file size/adherence concerns.
4. Git docs for generated/artifact boundary.

**Recent developments:**
- Empirical fuzzing of coding agents is beginning to catalog real-world anomalous behaviors, e.g. ABTest arXiv 2604.03362.

---

## E. Teaching considerations

**Where students get stuck:**
- They treat the checklist as judgment rather than diagnosis.
- They fix low-impact items first because they are easy.

**Analogies and framings that work:**
- This is a preflight checklist, not a moral inventory.

**Exercises:**
- Run the checklist on one project and rank fixes by risk reduction per hour.
- Pair audit with a before/after folder listing.

---

## Local library cross-references

- `_lib_ai-gigo-llm-toc.md`
- `_lib_ai-software-engineering-at-google-lessons-learned-from-programming-over-time.md`

