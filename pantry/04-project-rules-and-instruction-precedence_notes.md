# Research Notes: Chapter 04 - Project Rules and Instruction Precedence

**Source:** TIKTOC.md chapter entry
**Notes file:** 04-project-rules-and-instruction-precedence_notes.md
**Corresponding chapter:** chapters/04-project-rules-and-instruction-precedence.md (not yet written)
**Generated:** 2026-06-14

---

## Chapter summary from TIKTOC.md

Project rules need explicit precedence because each tool loads and resolves instruction files differently. The chapter covers `PROJECT_RULES.md`, `AGENTS.md`, `CLAUDE.md`, Cursor rules, Gemini, Aider, and advisory vs. enforced rules.

---

## A. Conceptual foundations

### Instruction files are context, not hard enforcement

Claude Code's memory docs state that CLAUDE.md and auto memory are loaded as context, not enforced configuration; hard blocking requires mechanisms such as hooks or managed settings. This distinction should be generalized: instruction files shape behavior but do not guarantee compliance.

**Common misconception:** "If I put it in the rules file, the tool cannot violate it." Rules are guidance unless backed by permissions, hooks, tests, or review gates.

**Worked example:** "Never delete files" in `AGENTS.md` is advisory. A pre-tool hook that blocks `rm` is enforcement.

**Source(s):** Claude Code memory docs, https://code.claude.com/docs/en/memory

### Precedence models differ

AGENTS.md describes nearest-file-wins behavior for nested files. Claude Code concatenates CLAUDE.md files across scopes and directory paths. Codex documents AGENTS.md use. Cursor, Gemini, Aider, and GitHub Copilot each have their own configuration conventions. The portable fix is explicit project-local precedence text plus adapters.

**Common misconception:** "My Claude setup is portable." It is portable only if other tools actually load the same content.

**Worked example:** Put shared rules in `AGENTS.md`; make `CLAUDE.md` contain `@AGENTS.md`; configure Aider to read it; optionally mirror into `GEMINI.md`.

**Source(s):** agents.md, https://agents.md/; Codex AGENTS.md docs, https://developers.openai.com/codex/guides/agents-md; Aider conventions, https://aider.chat/docs/usage/conventions.html

### Thin adapters prevent drift

The strongest pattern is one canonical instruction source plus thin tool-specific adapters. This prevents five files from gradually saying different things.

**Common misconception:** "Every tool needs its own fully tailored instruction file." Tailoring is useful only for tool-specific behavior; core rules should not be duplicated.

**Worked example:** `AGENTS.md` holds source-of-truth rules. `CLAUDE.md` imports it and adds "Use plan mode before edits under src/billing." This keeps shared and tool-specific content separate.

**Source(s):** Claude Code docs recommend importing `AGENTS.md` into `CLAUDE.md` where both are used.

---

## B. Domain examples and cases

### Case 1: No-delete rule

A project wants "archive, never delete." In `PROJECT_RULES.md`, it is a rule. In Claude, a hook can enforce it. In other tools, it may need shell wrappers, permission modes, or review discipline.

### Case 2: Team rules vs. personal rules

A personal preference such as "use short summaries" should not override a project rule such as "never modify production migrations without approval."

### Failure case: duplicated rules drift

`CLAUDE.md` says output to `outputs/`; `.cursor/rules` says output to `dist/`; Aider reads neither. The result is tool-dependent behavior.

---

## C. Connections and dependencies

**Prerequisites:**
- Chapter 3 manifest tiers.

**Unlocks:**
- Chapter 8 cross-tool workflow.
- Chapter 11 file safety.
- Chapter 15 measurement of rules effectiveness.

**Adjacent chapter connections:**
- Chapter 3: what to read.
- Chapter 5: how bloated rules become fixed context cost.

---

## D. Current state of the field

**Settled:**
- Major tools use persistent instruction files, but file names and precedence differ.
- Instruction files consume context and should be concise.

**Contested or emerging:**
- AGENTS.md is becoming a cross-agent standard, but not every tool treats it natively.
- Empirical evidence on whether instruction files improve outcomes is still developing and mixed.

**Key references:**
1. Claude Code memory docs - load order, AGENTS import, concision target.
2. Codex AGENTS.md docs - OpenAI's guidance for repo instructions.
3. agents.md - portable project instruction standard.
4. Aider conventions docs - explicit read file pattern.

**Recent developments:**
- Agentic AI Foundation makes AGENTS.md a more credible portability target.
- Empirical AGENTS.md studies are starting to test runtime, token, and success impacts.

---

## E. Teaching considerations

**Where students get stuck:**
- They confuse "loaded" with "enforced."
- They create one giant rules file instead of scoped modules.

**Analogies and framings that work:**
- Rules files are signs on the road; hooks/permissions are guardrails.

**Exercises:**
- Trace where one rule lives across all tools a reader uses.
- Convert a duplicated CLAUDE/Cursor/Aider setup into `AGENTS.md` plus adapters.

---

## Local library cross-references

- `_lib_ai-claude-ai-vs-claude-code-vs-claude-cowork-which-is-the-right-tool-for-your-workflow-automation.md`
- `_lib_ai-claude-code-the-definitive-guide-to-agentic-development.md`

