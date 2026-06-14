# Research Notes: Chapter 08 - One Folder, Many Tools: Making Cross-Tool Workflows Work

**Source:** TIKTOC.md chapter entry
**Notes file:** 08-one-folder-many-tools-making-cross-tool-workflows-work_notes.md
**Corresponding chapter:** chapters/08-one-folder-many-tools-making-cross-tool-workflows-work.md (not yet written)
**Generated:** 2026-06-14

---

## Chapter summary from TIKTOC.md

The same folder can serve Claude Code, Codex, Cursor, Gemini CLI, Aider, and other agents if `AGENTS.md` or a similar canonical file is the source of truth and tool-specific files are thin shims.

---

## A. Conceptual foundations

### Portable core, tool-specific adapters

The portable layer is plain files and directories. Tool adapters are `CLAUDE.md`, `GEMINI.md`, `.cursor/rules`, `.aider.conf.yml`, and other tool-specific entry points. The core should change rarely; adapters should be thin.

**Common misconception:** "Tool agnostic means no tool-specific files." Tool agnostic means the tool-specific files do not contain independent truth.

**Worked example:** `AGENTS.md` holds the core. `CLAUDE.md` imports it. `.aider.conf.yml` reads it. Gemini is configured to use the same context file or receives a short `GEMINI.md` adapter.

**Source(s):** agents.md; Claude Code memory docs; Aider conventions; Codex AGENTS.md docs.

### Reference, bridge, compile

There are three robustness levels. Reference means one file tells users to read another. Bridge means a tool-specific file imports or points to the canonical file. Compile means a build script generates adapters from shared modules.

**Common misconception:** "Symlinks solve it." Symlinks can be fragile across Windows/team environments and do not allow tool-specific overlays.

**Worked example:** A repo with generated `AGENTS.md` and `CLAUDE.md` from `instructions/` is a compile strategy.

**Source(s):** Claude docs discuss `@AGENTS.md` import and note Windows symlink caveats.

### Portability matrix thinking

Every pattern should be classified: fully portable, portable with adaptation, or tool-specific. Folder structure and status files are portable. Hooks and compaction commands are tool-specific.

**Common misconception:** "If a pattern is good in one agent, it is good everywhere." It may depend on that agent's loading, permissions, or UI.

**Worked example:** "Never delete" is portable as a rule; a Claude PreToolUse hook is not portable.

**Source(s):** Claude hooks docs; Codex docs; Aider docs.

---

## B. Domain examples and cases

### Case 1: Generated instruction pipeline

The Reallocation Engine's generated `AGENTS.md` and `CLAUDE.md` pattern is a good local model for compile-based adapters.

### Case 2: Team member uses Aider

If Aider does not auto-read AGENTS.md, `.aider.conf.yml` can list it as a read-only convention file.

### Failure case: parallel hand-written files

Manual `CLAUDE.md`, `GEMINI.md`, and Cursor rules drift. Tool behavior becomes inconsistent and impossible to debug.

---

## C. Connections and dependencies

**Prerequisites:**
- Chapters 2-4 setup files.

**Unlocks:**
- Chapter 12 anti-pattern "depending on tool-specific behavior."
- Chapter 15 measuring whether rules help.

**Adjacent chapter connections:**
- Chapter 7: tool-specific compaction commands vs portable handoffs.
- Chapter 9: MCP is cross-tool in concept but client-specific in configuration.

---

## D. Current state of the field

**Settled:**
- Different tools use different instruction entry points.
- AGENTS.md is the strongest current portable candidate.

**Contested or emerging:**
- No complete cross-vendor instruction precedence standard exists.
- Tool support for AGENTS.md is expanding but not uniform.

**Key references:**
1. agents.md.
2. Claude Code memory docs.
3. OpenAI Codex AGENTS.md docs.
4. Aider conventions docs.

**Recent developments:**
- Agentic AI Foundation stewardship of AGENTS.md and MCP increases pressure toward interoperability.

---

## E. Teaching considerations

**Where students get stuck:**
- They copy the same rules into multiple files and forget which is canonical.
- They overuse symlinks.

**Analogies and framings that work:**
- Canonical source plus adapters is like one manuscript exported to Kindle, PDF, and HTML.

**Exercises:**
- Inventory every instruction file in a project and mark canonical/adapter/generated.
- Convert two duplicated files into one source plus one adapter.

---

## Local library cross-references

- `_lib_ai-claude-ai-vs-claude-code-vs-claude-cowork-which-is-the-right-tool-for-your-workflow-automation.md`
- `_lib_ai-claude-cowork-capabilities.md`

