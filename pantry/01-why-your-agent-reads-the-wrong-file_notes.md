# Research Notes: Chapter 01 - Why Your Agent Reads the Wrong File

**Source:** TIKTOC.md chapter entry
**Notes file:** 01-why-your-agent-reads-the-wrong-file_notes.md
**Corresponding chapter:** chapters/01-why-your-agent-reads-the-wrong-file.md (not yet written)
**Generated:** 2026-06-14

---

## Chapter summary from TIKTOC.md

The agent does not know which files are canonical. It infers from folder names, file dates, and naming conventions, and a messy structure actively misleads it. This chapter explains wrong canonical file selection, over-broad reading, archived-vs-current confusion, attention budget, and context rot.

---

## A. Conceptual foundations

### Agents infer context from structure

An agent working in a filesystem does not begin with the human maintainer's mental model. It sees path names, filenames, recency, file sizes, imported instruction files, and tool output. Anthropic's context-engineering guidance explicitly treats file paths, naming conventions, hierarchy, and timestamps as meaningful metadata for agents, not just storage details. That makes folder design part of the interface.

**Common misconception:** "The agent will read everything and figure it out." In practice, reading everything wastes attention and increases the chance that old or adjacent material becomes a distractor.

**Worked example:** Two files sit beside each other: `proposal.md` and `proposal-old.md`. The agent summarizes `proposal-old.md` because it has a more explicit title or recent timestamp. Moving old material to `archive/` changes the agent's likely retrieval path.

**Source(s):** Anthropic, "Effective context engineering for AI agents," https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents

### Context rot is gradual, not a hard limit

Chroma's 2025 context-rot report tested 18 models and found that model performance becomes less reliable as input length grows, even on controlled tasks. The important teaching point is that degradation begins before a formal context-window limit is reached. Extra irrelevant or similar material acts like noise.

**Common misconception:** "I am fine until the context window is full." The better rule is: every loaded token competes with every other token for attention.

**Worked example:** A 300-token direct question is answered correctly. The same question embedded in a large folder dump becomes less reliable because distractor context competes with the answer.

**Source(s):** Chroma, "Context Rot," https://www.trychroma.com/research/context-rot

### Canonical-vs-archive confusion

The chapter should give the reader a vocabulary for "the agent read the wrong file" as a structural failure. The clean distinction is: canonical files are current sources of truth; archived files are recoverable history; generated outputs are products, not inputs.

**Common misconception:** "Archived means old in the filename." Agents respond much better to physical boundaries such as `archive/`, `current/`, and `outputs/`.

**Worked example:** In a writing repo, `draft-final.md`, `draft-final-v2.md`, and `draft-final-real.md` are all in one folder. The fix is not a naming game; it is `current/chapter.md` plus `archive/2026-06-old-drafts/`.

**Source(s):** Anthropic context-engineering guidance; Git ignore docs for separating generated artifacts, https://git-scm.com/docs/gitignore

---

## B. Domain examples and cases

### Case 1: Writing project with old drafts

Situation: a book folder has current drafts, older drafts, generated exports, and research notes in one directory. The agent uses an old draft as source. The concept explains why physical separation matters more than repeated prompting.

### Case 2: Code project with generated output

Situation: a generated bundle or API output sits next to source code. The agent edits generated output, not source. This illustrates why `build/` and `outputs/` must be marked non-canonical.

### Failure case: "Clean this up"

Vague cleanup prompts encourage the agent to infer intent. If the project gives weak structural signals, "cleanup" can become deletion, renaming, or moving current files into irrelevant places.

---

## C. Connections and dependencies

**Prerequisites:**
- Basic terminal and folder literacy - reader must understand path structure.
- Basic agent use - reader must have seen a tool read files or search the repo.

**Unlocks:**
- Chapter 2 - explains why the greenfield structure works.
- Chapter 3 - motivates the manifest as a map.
- Chapter 5 - connects wrong-file failures to context cost.

**Adjacent chapter connections:**
- Chapter 2: moves from diagnosis to clean folder design.
- Chapter 3: adds an explicit map over the folder design.

---

## D. Current state of the field

**Settled:**
- Long context is not uniformly reliable; context length and distractors matter.
- File paths and naming conventions are useful metadata for agents.

**Contested or emerging:**
- How much structure should be enforced by convention versus tool-native ignore files remains unsettled.
- Bigger context windows reduce some pressure but do not remove context rot.

**Key references:**
1. Anthropic, "Effective context engineering for AI agents" - core source for attention budget, folder metadata, just-in-time context.
2. Chroma, "Context Rot" - empirical basis for degradation with long context.
3. Git, `gitignore` documentation - useful for teaching generated/non-source separation.

**Recent developments:**
- Context-engineering language has replaced narrow "prompt engineering" for agent work.
- Agent tools now increasingly support persistent instruction files, but they still need clean filesystem signals.

---

## E. Teaching considerations

**Where students get stuck:**
- They blame the model rather than the folder.
- They assume naming files "old" or "final" is enough.

**Analogies and framings that work:**
- The filesystem is a map; the agent is a hurried visitor. If the map puts current files and old files in one room, the visitor guesses.

**Exercises:**
- Give a messy file listing and ask which file the agent is likely to use.
- Have readers redesign one real folder into `current/`, `archive/`, `outputs/`, and `research/`.

---

## Local library cross-references

- `_lib_ai-claude-code-the-definitive-guide-to-agentic-development.md`
- `_lib_ai-nbb-prompt-architecture-the-power-of-the-template-pattern.md`

