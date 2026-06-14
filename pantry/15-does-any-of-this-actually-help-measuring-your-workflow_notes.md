# Research Notes: Chapter 15 - Does Any of This Actually Help? Measuring Your Workflow

**Source:** TIKTOC.md chapter entry
**Notes file:** 15-does-any-of-this-actually-help-measuring-your-workflow_notes.md
**Corresponding chapter:** chapters/15-does-any-of-this-actually-help-measuring-your-workflow.md (not yet written)
**Generated:** 2026-06-14

---

## Chapter summary from TIKTOC.md

The honest chapter: instruction files may not uniformly improve outcomes. Readers should measure whether their rules, manifests, and workflows improve acceptance rate, edits after, time to valid diff, token cost, and risky behavior.

---

## A. Conceptual foundations

### Rules files are measurable artifacts

Instruction files consume context and should earn that cost. They should be evaluated like code: do they prevent known failures, improve runtime, reduce rework, or clarify behavior?

**Common misconception:** "More rules are always better." More rules can add fixed cost and contradictions.

**Worked example:** Remove three style rules that never affect output; keep one safety rule that prevents deletion.

**Source(s):** Claude memory docs on concise instructions; empirical AGENTS.md studies.

### Mini-benchmarking

A practical benchmark should compare with-rules and without-rules conditions across a small task suite: repo summary, bug fix, multi-file feature, test repair, and security-sensitive change.

**Common misconception:** "Anecdotal success proves the system works." The same task needs comparable conditions.

**Worked example:** Run a narrow bug fix twice in a disposable branch, once with `AGENTS.md`, once without, record time, tokens, acceptance, and risky edits.

**Source(s):** "On the Impact of AGENTS.md Files..." arXiv 2601.20404; ABTest arXiv 2604.03362.

### Mixed evidence is useful, not threatening

The chapter should avoid advocacy-only framing. If some studies find neutral or negative adherence effects and others find efficiency gains, the conclusion is not "rules are bad" or "rules are magic." The conclusion is: measure locally and prune.

**Common misconception:** "One paper settles the question." Tool versions, repos, task types, and metrics differ.

**Worked example:** A rules file may reduce runtime for setup-heavy tasks but not improve correctness for algorithmic tasks.

**Source(s):** arXiv 2509.14744 on Claude manifests; arXiv 2601.20404 on AGENTS.md efficiency; ABTest 2604.03362.

---

## B. Domain examples and cases

### Case 1: AGENTS.md improves efficiency but not correctness

The agent spends less time discovering commands but still needs tests to catch logic errors.

### Case 2: Rules file hurts by being stale

Old build command in rules causes repeated failures. Removing/updating the rule improves outcomes.

### Failure case: measuring only vibes

The reader says "it feels better" but has no acceptance or token data. The chapter should require a simple table.

---

## C. Connections and dependencies

**Prerequisites:**
- Chapter 3 manifests.
- Chapter 4 rules and precedence.
- Chapter 5 context cost.

**Unlocks:**
- A maintainable post-book practice: prune, test, and improve the workflow.

**Adjacent chapter connections:**
- Chapter 14: governance controls should also be tested.
- Back matter: references and update cadence.

---

## D. Current state of the field

**Settled:**
- Instruction files are widespread and measurable.
- Agent behavior varies across tools and tasks.

**Contested or emerging:**
- The net effect of instruction files on task success is not settled.
- Ideal benchmark design for local agent workflows is still developing.

**Key references:**
1. Lulla et al., "On the Impact of AGENTS.md Files on the Efficiency of AI Coding Agents," arXiv 2601.20404.
2. Chatlatanagulchai et al., "On the Use of Agentic Coding Manifests," arXiv 2509.14744.
3. Dai et al., "ABTest," arXiv 2604.03362.
4. Claude memory docs for instruction concision.

**Recent developments:**
- 2025-2026 research moved from anecdotal "best practices" toward empirical evaluation of manifests, failure reports, and agent behavior.

---

## E. Teaching considerations

**Where students get stuck:**
- They resist removing rules because every rule feels protective.
- They measure only output quality, not cost or risk.

**Analogies and framings that work:**
- A rules file is an employee handbook. If it is long, stale, and unenforced, it is not governance; it is clutter.

**Exercises:**
- Run the five-task mini-benchmark with and without rules.
- Review a rules file as a PR: keep, revise, delete, or enforce.

---

## Local library cross-references

- `_lib_ai-software-engineering-at-google-lessons-learned-from-programming-over-time.md`
- `_lib_ai-gigo-llm-toc.md`

