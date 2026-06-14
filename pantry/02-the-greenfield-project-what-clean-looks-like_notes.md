# Research Notes: Chapter 02 - The Greenfield Project: What Clean Looks Like

**Source:** TIKTOC.md chapter entry
**Notes file:** 02-the-greenfield-project-what-clean-looks-like_notes.md
**Corresponding chapter:** chapters/02-the-greenfield-project-what-clean-looks-like.md (not yet written)
**Generated:** 2026-06-14

---

## Chapter summary from TIKTOC.md

A self-describing folder structure lets the agent tell canonical from transient without being told, because folder names act as metadata. The chapter teaches workspace/project/source/current/research/staging/build/outputs/archive separation.

---

## A. Conceptual foundations

### Folder taxonomy as interface design

The greenfield structure is not primarily about neatness. It is an interface for human and agent navigation. The highest-value distinction is source vs. generated vs. archived vs. in-progress. The recommended structure gives agents strong path-level signals before they read content.

**Common misconception:** "Any sensible folder names are fine." The key is not taste; it is unambiguous role separation.

**Worked example:** Create `src/`, `current/`, `research/`, `staging/`, `build/`, `outputs/`, and `archive/` before any generated files exist. The empty folders act as rails when work starts.

**Source(s):** Anthropic context engineering; Git ignore docs.

### One bounded project per folder

An agent pointed at a large parent folder must infer project boundaries. For CLI-agnostic work, a bounded folder is the portable safety boundary. Multi-project workflows should use a project index or multi-root workspace rather than one giant mixed directory.

**Common misconception:** "The agent can just search." Search across unrelated projects introduces topically similar distractors.

**Worked example:** A parent `books/` folder contains 20 books. The correct book has its own project root with `TIKTOC.md`, `chapters/`, and `pantry/`; the agent should not have to scan sibling books.

**Source(s):** Chroma context rot; Anthropic folder metadata guidance.

### Generated artifacts are not source

`build/`, `output/`, and `outputs/` need explicit treatment because agents often see generated files as useful examples. They are useful for inspection, but dangerous as source of truth.

**Common misconception:** "If it is the final PDF/export/report, it must be canonical." The canonical layer is what can regenerate the output.

**Worked example:** A Markdown book source generates EPUB/PDF into `output/`. The agent should edit `chapters/`, not `output/book.html`.

**Source(s):** Git ignore documentation; clig.dev style of stdout/generated distinction can be discussed as analogy if needed.

---

## B. Domain examples and cases

### Case 1: Book project

Use this repo as an example: `chapters/` is source, `pantry/` is research, `output/` is generated, `images/` and `d3/` are assets. The chapter can show the retrofit from placeholder book scaffold to agent-ready book workspace.

### Case 2: Software repo

`src/` source, `tests/` validation, `docs/` reference, `dist/` generated, `.ai/` machine-readable agent metadata. This illustrates that the pattern transfers outside writing.

### Failure case: flat "AI project" folder

Everything in one folder - prompts, logs, generated summaries, old versions, and active source - causes wrong-file use, over-reading, and accidental overwrite.

---

## C. Connections and dependencies

**Prerequisites:**
- Chapter 1 failure mechanism.

**Unlocks:**
- Chapter 3 manifest tiers rely on the folder taxonomy.
- Chapter 11 file safety relies on archive/output separation.

**Adjacent chapter connections:**
- Chapter 1: why structure matters.
- Chapter 3: how to index the structure.

---

## D. Current state of the field

**Settled:**
- Agents benefit from path and naming metadata.
- Generated artifacts should be separated from source and often ignored by version control.

**Contested or emerging:**
- Whether to standardize exact names (`outputs/` vs. `output/`) is less important than documenting semantics.
- `.ai/` is a proposed portability layer, not a formal vendor standard.

**Key references:**
1. Anthropic, "Effective context engineering for AI agents."
2. Git, `gitignore` documentation.
3. agents.md - for the idea that repo-level agent instructions belong beside source.

**Recent developments:**
- AI coding tools increasingly search and edit whole repos; folder boundaries now affect agent behavior, not just human organization.

---

## E. Teaching considerations

**Where students get stuck:**
- They overbuild the structure before they understand the distinction between source and output.
- They resist moving old files because archive feels like deletion.

**Analogies and framings that work:**
- A restaurant kitchen: pantry, prep station, finished plates, trash/recycling, and archive are different zones. Mixing them makes mistakes inevitable.

**Exercises:**
- Give a messy repo and ask readers to assign each file to a destination.
- Have readers run `find . -maxdepth 2` and label every top-level directory by role.

---

## Local library cross-references

- `_lib_ai-gigo-llm-toc.md`
- `_lib_ai-software-engineering-at-google-lessons-learned-from-programming-over-time.md`

