# Research Notes: Chapter 10 - Agent Workflow Patterns That Actually Work

**Source:** TIKTOC.md chapter entry
**Notes file:** 10-agent-workflow-patterns-that-actually-work_notes.md
**Corresponding chapter:** chapters/10-agent-workflow-patterns-that-actually-work.md (not yet written)
**Generated:** 2026-06-14

---

## Chapter summary from TIKTOC.md

Nine tool-agnostic workflow patterns reduce per-task and accumulated cost: builder-validator, researcher-writer-editor, planner-executor-reviewer, subagents, staging-before-output, approval gates, destructive gates, diff-first, and test-before-write.

---

## A. Conceptual foundations

### Workflow patterns over giant prompts

Anthropic's "Building effective agents" distinguishes simpler workflows from more autonomous agents and emphasizes composing patterns such as prompt chaining, routing, parallelization, orchestrator-workers, and evaluator-optimizer. For this book, the practical translation is: use a pattern when it clarifies roles and reduces self-grading.

**Common misconception:** "A single giant prompt is simpler." It is simpler to write, but harder to validate.

**Worked example:** Researcher gathers sources, writer drafts, editor checks source coverage. Each phase has a narrower context.

**Source(s):** Anthropic, "Building Effective AI Agents," https://www.anthropic.com/engineering/building-effective-agents

### Builder-validator

The builder creates; the validator checks against explicit criteria. The validator should not be asked to "find anything wrong" without scope or it may over-report.

**Common misconception:** "The agent can critique itself in the same context." It often rationalizes its own output.

**Worked example:** Builder writes a chapter note. Validator sees TIKTOC spec, notes file, and quality bar, then returns only missing requirements.

**Source(s):** Anthropic evaluator-optimizer pattern.

### Test-before-write and diff-first

For code, tests are a concrete evaluator. For writing, checklists and rubrics are equivalent. Diff-first reduces blast radius by making the intended change visible before execution.

**Common misconception:** "Validation is only for code." A chapter can be validated against anatomy, sources, and exercises.

**Worked example:** Before changing 12 files, the agent lists intended files and waits for approval.

**Source(s):** Claude Code best practices; Anthropic building effective agents.

---

## B. Domain examples and cases

### Case 1: Document generation

Researcher writes notes to `pantry/`, writer drafts to `chapters/`, validator checks against `TIKTOC.md`.

### Case 2: Code change

Planner explores read-only; executor patches; reviewer checks diff and tests.

### Failure case: self-grading

One prompt asks the agent to write, review, and approve. It makes small edits and declares success without independent validation.

---

## C. Connections and dependencies

**Prerequisites:**
- Chapter 5 cost types.
- Chapter 6 state discipline.

**Unlocks:**
- Chapter 11 gates.
- Chapter 14 validator passes for security.

**Adjacent chapter connections:**
- Chapter 9: use subagents/workflows to isolate MCP-heavy exploration.
- Chapter 11: file safety makes workflow patterns safe.

---

## D. Current state of the field

**Settled:**
- Patterned agent workflows outperform amorphous "do everything" prompting for complex tasks.
- Evaluator/optimizer and orchestrator/worker patterns are widely recommended.

**Contested or emerging:**
- How much autonomy to give subagents remains context-dependent.
- Human approval gates can improve safety but slow flow if overused.

**Key references:**
1. Anthropic, "Building Effective AI Agents."
2. Anthropic, "Effective context engineering for AI agents."
3. Claude Code best practices.

**Recent developments:**
- Coding tools increasingly expose plan modes, review modes, subagents, and worktrees, but the portable pattern is still plain-language role separation.

---

## E. Teaching considerations

**Where students get stuck:**
- They overuse agents for tasks that need a simple command.
- They under-specify validator criteria.

**Analogies and framings that work:**
- Builder and inspector are different jobs on a construction site.

**Exercises:**
- Rewrite a failed one-shot prompt as researcher-writer-editor.
- Create a validator checklist for a non-code deliverable.

---

## Local library cross-references

- `_lib_ai-nbb-prompt-architecture-the-power-of-the-template-pattern.md`
- `_lib_ai-prompt-engineering-textbook.md`

