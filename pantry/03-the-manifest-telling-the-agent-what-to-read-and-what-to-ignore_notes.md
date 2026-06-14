# Research Notes: Chapter 03 - The Manifest: Telling the Agent What to Read and What to Ignore

**Source:** TIKTOC.md chapter entry
**Notes file:** 03-the-manifest-telling-the-agent-what-to-read-and-what-to-ignore_notes.md
**Corresponding chapter:** chapters/03-the-manifest-telling-the-agent-what-to-read-and-what-to-ignore.md (not yet written)
**Generated:** 2026-06-14

---

## Chapter summary from TIKTOC.md

A manifest is a short index that prevents agents from reading the whole project on every task. It defines Tier 1 canonical files, Tier 2 task-relevant files, and Tier 3 archive/generated files to ignore unless requested.

---

## A. Conceptual foundations

### Manifest as progressive disclosure

A manifest lets a project show a small table of contents before loading content. It is a human-readable version of progressive disclosure: always read a small index, then retrieve relevant files on demand.

**Common misconception:** "The manifest is another instruction file." It is an index, not a rulebook or content dump.

**Worked example:** `_MANIFEST.md` tells the agent: read `PROJECT_RULES.md` and `status.md`; use `research/current/` only for evidence checks; ignore `archive/` unless asked.

**Source(s):** Anthropic Skills progressive disclosure model; Claude Code memory docs; Aider repo map.

### Native analogues: Skills, memory, repo maps

Anthropic Skills use a small metadata/body/resources loading pattern. Claude Code auto memory loads a bounded index at startup and pulls detailed memory on demand. Aider's repo map uses code structure and token budgeting to give the model a compact map of a repository.

**Common misconception:** "Manifest files are invented bureaucracy." Tool vendors independently implement similar map-first designs.

**Worked example:** Aider's repo map gives signatures and important files without loading every source file. `_MANIFEST.md` does the same at the workflow level.

**Source(s):** Claude memory docs, https://code.claude.com/docs/en/memory; Aider repo map, https://aider.chat/docs/repomap.html

### Manifest staleness

A stale manifest is actively harmful because it gives the agent confident wrong instructions about what matters. The maintenance rule should be simple: update the manifest when Tier 1 files change, when folder roles change, or when a new generated/private area appears.

**Common misconception:** "Once written, a manifest is done." It is a living index.

**Worked example:** If `outline.md` is replaced by `TIKTOC.md` as the canonical chapter plan, the manifest must change or agents will keep reading the wrong file.

**Source(s):** Anthropic's warning about stale indexing and preference for just-in-time file retrieval.

---

## B. Domain examples and cases

### Case 1: Book research pantry

For this book, a manifest can declare `TIKTOC.md` canonical, `pantry/` notes task-relevant, and `output/` generated. Without that, an agent might treat old output as source.

### Case 2: Code repo with generated clients

Generated API clients should be Tier 3 unless a task is specifically about generated output. The OpenAPI spec or source schema is Tier 1/2.

### Failure case: manifest as content dump

A manifest with long prose descriptions of every file becomes another bloated always-read file. The fix is tables, not narrative.

---

## C. Connections and dependencies

**Prerequisites:**
- Chapter 2's folder taxonomy.

**Unlocks:**
- Chapter 4 project rules can refer to manifest tiers.
- Chapter 6 session startup can read Tier 1 only.
- Chapter 13 failure catalog can diagnose manifest failures.

**Adjacent chapter connections:**
- Chapter 2: structure.
- Chapter 4: behavior rules and precedence.

---

## D. Current state of the field

**Settled:**
- Map-first approaches reduce unnecessary context loading.
- Agents need bounded, high-signal startup context.

**Contested or emerging:**
- `_MANIFEST.md` is a convention, not a standard.
- `.ai/manifest.yaml` is useful for automation but not broadly standardized.

**Key references:**
1. Claude Code memory docs - CLAUDE.md and auto memory loading.
2. Aider repo map docs - automated map under token budget.
3. agents.md - cross-agent instruction file standard.

**Recent developments:**
- Agentic AI Foundation stewardship of AGENTS.md strengthens the case for portable repo instructions, but not for any one manifest schema.

---

## E. Teaching considerations

**Where students get stuck:**
- They put too much text into the manifest.
- They classify outputs as canonical because humans read them.

**Analogies and framings that work:**
- A manifest is an airport signboard: it tells you where to go, but it is not the destination.

**Exercises:**
- Write a manifest for an existing project in under 15 minutes.
- Delete half the words from the manifest while preserving every decision.

---

## Local library cross-references

- `_lib_ai-nbb-prompt-architecture-the-power-of-the-template-pattern.md`
- `_lib_ai-claude-code-the-definitive-guide-to-agentic-development.md`

