# TIKTOC.md
## CLI-Agnostic AI Tooling for Local Project Workflows

**Series:** AI+1 Practitioner Handbook Series · Bear Brown & Company
**Author:** Nik Bear Brown · ni.brown@neu.edu · Bear Brown & Company
**Format:** $1 Kindle / Kindle Unlimited
**Distribution:** Bear Brown & Company independent publishing
**Version:** 1.0
**Status:** Pre-drafting — all phases complete
**Source:** v1.1 research guide (June 2026, multi-source adversarial verification)

---

## Document Structure

1. Book Concept and Thesis
2. Learner Profile
3. Book Type and Deployment Specification
4. Field Positioning
5. Learning Outcomes
6. Sequencing Model
7. Three-Act Learning Arc
8. Prerequisite Map
9. Chapter-by-Chapter Specifications
10. Chapter Anatomy Template
11. Case Study and Worked Example Strategy
12. Contested Claims and Aging Risk
13. Market Positioning
14. Feature List
15. Out of Scope
16. Adoption Risk Register
17. Open Questions Log

---

# PART 1 — BOOK CONCEPT AND THESIS

## Book Concept Summary

> This book teaches **the diagnosis-and-intervention layer of CLI-based AI workflows — the decisions that require understanding context mechanics and that no tool's documentation covers cross-vendor** — to **daily users of Claude Code, Codex CLI, Cursor, Gemini CLI, and similar tools whose workflows are burning excess tokens, producing degraded results, or becoming unmaintainable**, by **presenting the filesystem as the durable, tool-agnostic operating system for AI work and every CLI as a replaceable adapter over it, with copy-paste templates for each intervention**, through **chapters organized by the problem the reader is experiencing right now, not by the field's conceptual logic**. It fills the gap left by vendor documentation (which covers one tool's controls) and single-tool books like Marco's *Agentic Coding with Claude Code* (which teaches Claude Code's features without explaining why sessions degrade or how to fix them across tools). It succeeds if the reader can **set up a greenfield project that any CLI agent navigates correctly, diagnose why a running session is degrading, and apply the right intervention — across whichever tool they are using**.

**One-sentence logline:**
Your AI workflow isn't broken because the model is bad — it's broken because the filesystem is a mess and the context window is eating itself, and this book shows you exactly how to fix both.

## Central Thesis

"This book argues that the failures most CLI AI users experience — degraded output quality, excess token spend, unmaintainable workflows, and results that vary unpredictably across tools — are context problems caused by poor filesystem structure and session hygiene, not model problems, and that the cure is treating the filesystem as the durable, tool-agnostic operating system for AI work and every CLI as a replaceable adapter over it, which matters because the tools will keep changing and the filesystem contract will not."

## Thesis Test

The TOC reflects the thesis at every level:

- **The Setup chapters** establish what clean looks like — the greenfield project structure that any agent navigates correctly without being told **✓**
- **The Diagnosis chapters** give the reader a failure-mode vocabulary and a map from symptom to structural cause **✓**
- **The Intervention chapters** provide copy-paste fixes that work because they are filesystem conventions, not tool-specific settings **✓**
- **The label discipline** (`[OFFICIAL]`, `[CONVENTION]`, `[INFERRED]`, `[AGNOSTIC]`) runs throughout every chapter, so the reader knows exactly how confident to be in each piece of advice — the one thing no vendor doc provides **✓**

**Thesis test: PASS**

---

# PART 2 — LEARNER PROFILE

## Primary Reader

A working practitioner who uses Claude Code, Codex CLI, Cursor, Gemini CLI, or a similar agent daily — for coding, writing, or research tasks — and whose workflows are visibly expensive, slow, or producing results that feel wrong without a clear diagnosis.

**Specific person:** A developer or technical writer who has been using Claude Code or Codex for three to six months, has built up a folder structure that made sense at the time, is now seeing sessions degrade mid-task, is spending more tokens than expected, and has no framework for diagnosing why.

**Secondary person:** Someone setting up a new project with an AI agent for the first time who wants to get the structure right before they build a mess.

## Prior Knowledge Assumed

- Comfortable working in a terminal
- Basic git (clone, commit, branch)
- Familiar with at least one CLI AI tool at the "I've used it" level
- Can read and write basic Markdown and YAML

## Prior Knowledge NOT Assumed

- Deep git internals or advanced branching
- MCP architecture or protocol details
- Prompt engineering theory
- Any specific vendor's advanced configuration

## Prior Misconceptions (what they think they know that is wrong)

1. "My session is degrading because I hit the context limit" — context rot is continuous and gradual, not a cliff; it starts degrading long before the window is full
2. "A bigger CLAUDE.md gives the agent more to work with" — a bloated instruction file loads on every turn and dilutes reasoning; it is one of the most common self-inflicted wounds
3. "Adding more MCP servers gives the agent more capability" — every schema loads on every turn before the agent types a word; more servers = more fixed context cost
4. "Ignore files keep secrets safe" — ignore files reduce context load; they are not a security boundary
5. "The agent always reads the right file" — agents infer canonical from folder names and timestamps; messy structure actively misleads them
6. "If my CLAUDE.md works in Claude Code, it'll work in Codex" — precedence models differ fundamentally across tools; what works in one tool may be silently ignored in another

## Motivation Type

**Primary:** Professional — they use these tools at work or in serious personal projects, the waste is real, and they want to fix it today.

**Secondary:** Craft — they suspect there is a right way to structure this work and they want to understand the principles, not just get the fix.

The practitioner handbook format honors the professional motivation: every chapter is organized around a problem the reader is experiencing, not around a concept the field has established.

## Prerequisite Map

| Prerequisite | Safe to assume? | If not: where addressed |
|---|---|---|
| Terminal comfort | Yes | — |
| Basic git | Yes | — |
| One CLI tool experience | Yes | — |
| Markdown / YAML basic reading | Yes | — |
| MCP architecture | No | Chapter 9 (just enough) |
| Prompt engineering theory | No | Not required — excluded by design |
| Advanced git (worktrees, hooks) | No | Chapter 13 (just enough) |
| Specific vendor internals | No | Each chapter covers relevant vendor detail inline |

**Front-loading decision:** MCP architecture and advanced git are the only non-excluded "No" prerequisites. Both are addressed at first use with a "just enough" treatment — no full chapter dedicated to prerequisites. The book assumes a practitioner who learns by doing, not by reading foundations first.

---

# PART 3 — BOOK TYPE AND DEPLOYMENT SPECIFICATION

## Book Type

**PRIMARY TYPE:** Practitioner handbook — organized by task/problem, not by concept. Each chapter is self-contained. The reader enters at the chapter that matches their current pain. No required reading order.

**NOT:** Course textbook (chapters are not sequential capability builds), field-defining monograph (no sustained argument to follow), reference work (opinionated about what to do, not exhaustive about what exists).

## Deployment Specification

**Primary adoption context:**
$1 Kindle / Kindle Unlimited. Individual purchase by working practitioners. Read out of sequence. Consulted when something is broken or when starting a new project.

**Secondary adoption context:**
Team onboarding documents. Engineering managers pointing new hires at specific chapters. Workshop companion for AI tooling sessions.

**What this book is NOT designed for:**
Cover-to-cover reading as a narrative (though the arc is coherent for those who do); graduate course adoption (too practical, not theoretical enough); vendor-specific deep dives (deliberately shallow on any one tool's internals).

**How the structure signals book type to a reader:**
Table of contents organized by problem/symptom, not by concept. Chapter titles answer "what is happening to me" not "what is this topic." Every chapter opens with a failure mode. Every chapter closes with a copy-paste fix.

---

# PART 4 — FIELD POSITIONING

## The Positioning Statement — Consolidated

The competitive landscape is clean:

- **Vendor documentation** covers one tool's controls. This book covers the cross-tool diagnosis layer.
- **Marco, *Agentic Coding with Claude Code*** teaches Claude Code's features. This book teaches why workflows fail and how to fix them across any tool.
- **"Beginners Bible" genre** (Sheldon, Baker/Evans) teaches prompting and use cases. This book teaches workflow architecture and failure diagnosis.
- **Vibecoding/101-things genre** gives tips for one tool. This book gives a transferable mental model.
- **The source research guide** (v1.1) tells you what is true. This book tells you what to do when something is broken.

**The gap this book fills:** No existing resource teaches the CLI-agnostic layer — the mental model and interventions that hold across Claude Code, Codex, Cursor, Gemini CLI, and whatever ships next year. Every vendor writes about their own tool. Nobody has written the cross-vendor diagnosis and repair manual.

## Positioning Statements by Competitor

**vs. Marco, *Agentic Coding with Claude Code* (Packt, 2026):**
"Unlike *Agentic Coding with Claude Code*, which teaches you how to drive Claude Code's controls — slash commands, CLAUDE.md, MCP, subagents — this book teaches you why your workflow is degrading and what to fix it, across whichever tool you are using today or will use next year."

**vs. Vendor documentation (Anthropic, OpenAI, Google):**
"Unlike vendor documentation, which tells you how each tool's own features work, this book tells you what the tools have in common, where they differ in ways that matter, and how to structure your work so it survives switching tools."

**vs. Beginners Bible genre:**
"Unlike general Claude AI introductions, which teach you what prompts to write, this book teaches you why your project folder is misleading the agent, why your session quality is dropping mid-task, and what to do about both — using templates you can copy and paste today."

**vs. The source research guide (v1.1):**
"The research guide tells you what is true about context engineering and cross-tool behavior, with source confidence labels on every claim. This book takes those findings and turns them into a diagnosis-and-repair manual organized by the problem you are experiencing right now."

---

# PART 5 — LEARNING OUTCOMES

## Outcome Map

| Chapter | Primary Bloom's Level | Assessable? | Core capability |
|---|---|---|---|
| 1 | Understand | Yes | Explain why agents infer canonical from structure |
| 2 | Apply | Yes | Build a greenfield project folder that any agent navigates correctly |
| 3 | Apply | Yes | Write a manifest that tells the agent what to read and what to ignore |
| 4 | Apply | Yes | Write project rules with an explicit precedence statement |
| 5 | Analyze | Yes | Diagnose which cost type is consuming context in a given session |
| 6 | Apply | Yes | Implement session hygiene and state file protocols |
| 7 | Analyze | Yes | Diagnose a degrading session and select the right compaction intervention |
| 8 | Apply | Yes | Make one folder work correctly across multiple CLI tools |
| 9 | Analyze | Yes | Diagnose MCP context cost and apply load-reduction interventions |
| 10 | Apply | Yes | Apply agent workflow patterns to a real task |
| 11 | Apply | Yes | Implement file safety rules and destructive-action gates |
| 12 | Evaluate | Yes | Assess a workflow against the anti-patterns checklist |
| 13 | Evaluate | Yes | Apply the failure-mode catalog to a real project |
| 14 | Evaluate | Yes | Assess governance and security posture for an agent deployment |
| 15 | Evaluate | Yes | Measure whether a rules file actually improves outcomes |

**Outcome distribution:** 2 Understand, 8 Apply, 3 Analyze, 2 Evaluate. Heavy Apply weighting is correct for a practitioner handbook — every chapter produces a deliverable the reader can use immediately.

---

# PART 6 — SEQUENCING MODEL

## Primary Model: Problem-to-Solution

Each chapter opens with the failure mode (the problem the reader is experiencing). The structural explanation arrives after the problem has made the reader need it. The fix follows the explanation. The copy-paste template closes the chapter.

**Justification against learner profile:** The primary reader is a working practitioner with a broken or expensive workflow. They do not read foundations first. They read the chapter that matches their pain. Problem-first framing is the only sequencing that works for this reader and this format.

**Where the model is most likely to break down:** Chapters 1–2 (the greenfield setup chapters). A reader who has never used a CLI agent and has no existing pain cannot enter via failure mode. These chapters are the one exception to problem-first — they open with "what clean looks like" rather than "what broken looks like," because the reader has nothing broken yet.

**Transition chapter:** Chapter 4 (Project Rules and Instruction Precedence) is the pivot from "what to build" (setup) to "why it matters" (diagnosis). It is the load-bearing connection between the greenfield section and the failure-diagnosis section.

---

# PART 7 — THREE-ACT LEARNING ARC

## Arc Statement

This book takes the reader from **a practitioner whose AI workflow is opaque, expensive, and tool-dependent** to **one who can set up any project correctly, diagnose any failure, and apply the right fix — in any CLI tool** by first establishing that the problems are structural and solvable (Act One: Setup), then building the diagnostic vocabulary and interventions piece by piece (Act Two: Diagnosis and Repair), then applying the full toolkit to the hard cases — multi-tool environments, MCP, governance, and measurement (Act Three: Advanced and Honest).

## Act One — Setup (Chapters 1–4)

**Starting state:** The reader understands that something is wrong but has no structural vocabulary for it.
**Ending state:** The reader has a greenfield project structure, a manifest, and project rules — the three artifacts that make any agent's behavior predictable.
**Inciting question:** "What does a project folder that works correctly actually look like?"
**Act One → Act Two transition:** The reader has a clean structure. Now they need to understand what breaks it over time.

## Act Two — Diagnosis and Repair (Chapters 5–11)

**Starting state:** The reader has a clean structure but their running sessions are still degrading.
**Ending state:** The reader can identify every major failure mode, name its structural cause, and apply the right intervention.
**Hardest conceptual moment:** Chapter 9 (MCP context cost) — the revelation that tool schemas load on every turn before the agent types a word is the single most counterintuitive finding in the research base.
**Act Two → Act Three transition:** The reader can diagnose and repair individual failures. Now they need to handle the hard cases: multi-tool environments, governance, and honest measurement.

## Act Three — Advanced and Honest (Chapters 12–15)

**Starting state:** The reader can handle the common failure modes.
**Ending state:** The reader can assess their own workflow against a complete checklist, apply governance controls, and — critically — measure whether their rules files are actually working.
**The transfer test:** Chapter 15 ("Does Any of This Actually Help?") is the honest chapter. It presents the empirical evidence that instruction files may not uniformly improve outcomes, gives the reader a measurement protocol, and earns the trust that advocacy-only framing would have spent.

---

# PART 8 — PREREQUISITE MAP

## Dependency Map

| Chapter | Depends on | Load-bearing? |
|---|---|---|
| 1 | Nothing | — |
| 2 | Ch. 1 | Yes — Ch. 2 builds the structure Ch. 1 explains |
| 3 | Ch. 2 | Yes — manifest assumes the folder structure exists |
| 4 | Ch. 3 | Yes — rules file assumes the manifest exists |
| 5 | Ch. 1 (conceptual) | Light — context cost types are self-contained |
| 6 | Ch. 5 | Yes — session hygiene assumes cost understanding |
| 7 | Ch. 5, 6 | Yes — compaction assumes hygiene protocols |
| 8 | Ch. 2, 3, 4 | Yes — multi-surface bridging assumes the setup exists |
| 9 | Ch. 5 | Yes — MCP cost is a specific cost type |
| 10 | Ch. 1 (conceptual) | Light — patterns are self-contained |
| 11 | Ch. 2, 3, 4 | Light — file safety extends the setup |
| 12 | Ch. 1–11 (survey) | Light — checklist format is self-contained |
| 13 | Ch. 5–11 | Light — failure catalog references earlier chapters |
| 14 | Ch. 2, 3, 4, 11 | Light — governance extends the setup |
| 15 | Ch. 3, 4 | Light — measurement targets rules files |

**The reader who skips chapters test:** A reader who enters at Chapter 9 (MCP cost) needs to understand "context cost types" from Chapter 5 but can get the key concept from the chapter's own opening. No chapter is fully incomprehensible without prior chapters — but Chapters 2, 3, 4 form a setup sequence that is most valuable read in order.

---

# PART 9 — CHAPTER-BY-CHAPTER SPECIFICATIONS

---

## ACT ONE — SETUP (Chapters 1–4)
*What clean looks like. The three artifacts that make agent behavior predictable.*

---

### CHAPTER 1 — Why Your Agent Reads the Wrong File

**One-line:** The agent doesn't know which files are canonical — it infers from folder names, file dates, and naming conventions, and a messy structure actively misleads it.

**Keyword audit:** PASS — "agent," "context," "canonical," "folder structure" are searchable terms; the title answers the reader's question directly.

**The problem it solves:** The reader has gotten wrong or stale output and suspects the agent read the wrong file, but doesn't understand the mechanism.

**Learning outcomes:**
1. (Understand) Explain why agents infer canonical file status from folder hierarchy and naming conventions rather than reading everything.
2. (Understand) Describe the three recurring failures — wrong canonical file, over-broad reading, archived-vs-current confusion — in structural terms.
3. (Apply) Identify which failure type is occurring in a given broken workflow.

**Chapter opening:** A session where the agent confidently uses an archived spec to answer a question about the current project. The fix is not a better prompt. The fix is a folder structure where "archived" is physically separated from "current."

**Core content blocks:**
1. How agents build context — folder names as metadata, timestamps as signals, naming conventions as inference
2. The three failure types: wrong canonical, over-broad, archived-vs-current
3. Why folder structure is the fix, not prompting
4. The attention budget: why reading broadly is not free even when it fits
5. Context rot: continuous degradation, not a cliff at the window limit

**Worked example:** A writing project where two drafts of the same document exist — one current, one archived — in the same folder. The agent uses the older one. The fix: physically separate `current/` from `archive/`. Before/after folder structure shown.

**Copy-paste template:**
```
# Why the agent read the wrong file — quick diagnosis
# Check: do you have old and current drafts in the same folder?
# Check: does your folder have a clearly named archive/ directory?
# Check: does your project have a _MANIFEST.md that names canonical files?
# If any answer is no: see Chapter 2 for the fix.
```

**Assessable exercises:**
1. Given a folder listing, identify which failure type is most likely occurring and why.
2. Describe the structural change that would fix it.

**Bridge:** You now understand the failure mechanism. Chapter 2 shows you the folder structure that prevents all three failure types from the start.

**Label discipline note:** Context rot finding is `[OFFICIAL]` (Chroma research). Attention budget framing is `[OFFICIAL]` (Anthropic). Three failure types are `[CONVENTION]` synthesized from practitioner write-ups.

---

### CHAPTER 2 — The Greenfield Project: What Clean Looks Like

**One-line:** A self-describing folder structure where the agent can tell canonical from transient without being told — because the folder names are the metadata.

**Keyword audit:** PASS — "greenfield," "project structure," "AI agent," "folder" are all searchable; title signals the deliverable.

**The problem it solves:** The reader is starting a new project (or wants to retrofit an existing one) and wants to get the structure right before it becomes a mess.

**Learning outcomes:**
1. (Apply) Build a project folder structure where canonical, transient, and archived files are physically separated.
2. (Apply) Name and assign each folder correctly using the canonical folder taxonomy.
3. (Evaluate) Assess whether an existing project structure would mislead an agent, and identify the highest-risk folders.

**Chapter opening:** The "vibing a mess" pattern — how most projects start. The developer prompts, the agent writes files, folders accumulate, and within weeks the agent is reading generated output as if it were source. The greenfield structure is the prevention.

**Core content blocks:**
1. The recommended structure — workspace, project, source, current, research, staging, build, outputs, archive
2. What each folder exists for — and what must NOT go there
3. Why `build/` and `outputs/` must never become source
4. One folder per bounded project — why mixing projects in one tree breaks context
5. `.gitignore` the generated layers — why this matters for both git and agents

**Full folder structure template:**
```
/workspace/
├── _shared/
│   ├── _system/
│   ├── _context/
│   ├── templates/
│   └── skills/
├── _PROJECT_INDEX.md
│
└── project-a/
    ├── AGENTS.md
    ├── _MANIFEST.md
    ├── PROJECT_RULES.md
    ├── status.md
    ├── session-handoff.md
    ├── .ai/
    │   ├── manifest.yaml
    │   ├── workflows/
    │   ├── schemas/
    │   ├── sessions/
    │   └── audit/
    ├── src/
    ├── current/
    ├── research/
    ├── templates/
    ├── staging/
    ├── build/
    ├── outputs/
    └── archive/
```

**Worked example:** An existing messy project retrofitted into the clean structure. Before: drafts, outputs, archived versions, and notes in one flat folder. After: each file in its correct location, with the agent's behavior improving immediately because `archive/` is now physically invisible to normal operation.

**Copy-paste template:** Full folder structure with one-line explanations for each folder. Ready to run `mkdir -p` commands provided.

**Assessable exercises:**
1. Given a messy existing project folder, assign each file to its correct location in the clean structure.
2. Name two files in your current most-used project that are in the wrong location and explain the risk.

**Bridge:** You have the structure. Now you need a file that tells the agent which parts of it are canonical and which to ignore. That file is the manifest.

**Label discipline note:** Folder-names-as-metadata is `[OFFICIAL]` (Anthropic). The specific folder names are `[CONVENTION]` assembled from practitioner practice and the `[INFERRED]` cross-tool synthesis. No tool ships this exact tree — the principles are vendor-backed, the names are yours to choose.

---

### CHAPTER 3 — The Manifest: Telling the Agent What to Read and What to Ignore

**One-line:** A two-minute file that prevents the agent from reading your entire project on every task — the index that makes just-in-time context loading possible.

**Keyword audit:** PASS — "manifest," "context loading," "AI agent," "AGENTS.md" are searchable; title signals the mechanism.

**The problem it solves:** The reader has a clean folder structure but the agent still reads too broadly — or reads the wrong tier of files — because there is no explicit map.

**Learning outcomes:**
1. (Understand) Explain what a manifest does and why it is high-leverage for context efficiency.
2. (Apply) Write a `_MANIFEST.md` with correct Tier 1 / Tier 2 / Tier 3 assignments for a real project.
3. (Apply) Write a `.ai/manifest.yaml` machine-readable twin.
4. (Analyze) Identify the single most dangerous failure mode of a manifest and explain the mitigation.

**Chapter opening:** A session where the agent reads a 200-file research archive looking for one relevant paper. The manifest would have told it "Tier 3 — ignore unless asked." The cost: 40 minutes and a bloated context that degraded the rest of the session.

**Core content blocks:**
1. What a manifest is and what it is not — index, not document
2. The three-tier structure — Canonical (always), Task-Relevant (on demand), Archive/Generated (ignore)
3. Native manifest implementations: Anthropic Skills `SKILL.md`, Claude Code `MEMORY.md`, Aider repo map — all are the same pattern
4. `AGENTS.md` as the cross-vendor standard
5. The staleness problem: why a manifest only helps if maintained

**`_MANIFEST.md` copy-paste template:**
```markdown
# _MANIFEST.md — read this first

> This file maps what to read and what to ignore. If it conflicts with what
> you find on disk, trust this file and flag the discrepancy.

## Tier 1 — Canonical (always read first)
| File | Purpose |
|------|---------|
| PROJECT_RULES.md | Project-specific rules and precedence |
| status.md | Current state, latest decisions, next actions |
| outline.md | Source of truth for structure |

## Tier 2 — Task-Relevant (load only when the task needs it)
| Folder | Use when |
|--------|----------|
| current/ | Editing active source material |
| research/current/ | Checking live research/evidence |
| templates/ | Producing a repeatable output |

## Tier 3 — Archive / Generated (ignore unless explicitly requested)
| Folder | Rule |
|--------|------|
| archive/ | Ignore unless I explicitly ask |
| build/ | Generated; never a source of truth |
| outputs/ | Finished deliverables; not working source |

_Last updated: YYYY-MM-DD — update whenever Tier 1 files change._
```

**`.ai/manifest.yaml` copy-paste template:**
```yaml
name: project-alpha
canonical: [PROJECT_RULES.md, status.md, outline.md]
task_relevant: [current/, research/current/, templates/]
ignore: [archive/, build/, outputs/]
entrypoints: { build: "make build", test: "make test" }
invariants:
  - "Never treat outputs/ or build/ as source."
  - "Move superseded files to archive/, never delete."
permissions:
  filesystem_scope: workspace-only
  network_allowlist: ["registry.npmjs.org"]
  forbidden: ["rm -rf", "git push --force"]
```

**Worked example:** A project with a well-maintained manifest vs. the same project without one. Token cost comparison at session start. The manifest reduces Tier 2 loading from "everything" to "what the task needs."

**Assessable exercises:**
1. Write a `_MANIFEST.md` for a project you currently work on. Assign every major folder to a tier with one-sentence justification.
2. Name the three conditions under which you should update the manifest. When did you last do each?

**Bridge:** The manifest tells the agent what to read. The project rules file tells it how to behave. Chapter 4 covers the rules file — including the one instruction every tool will honor: an explicit precedence statement.

**Label discipline note:** Three-tier structure and `_MANIFEST.md` are `[CONVENTION/INFERRED]`. `AGENTS.md` standard is `[OFFICIAL]` (Linux Foundation Agentic AI Foundation). Claude Code `MEMORY.md` 200-line limit is `[OFFICIAL]`. Static indexes going stale is `[OFFICIAL]` (Anthropic).

---

### CHAPTER 4 — Project Rules and Instruction Precedence

**One-line:** A `PROJECT_RULES.md` with an explicit precedence statement is the one instruction every tool will at least see — because precedence models differ fundamentally across tools and you can't trust any tool's default.

**Keyword audit:** PASS — "project rules," "instruction precedence," "CLAUDE.md," "AGENTS.md" are all searchable.

**The problem it solves:** The reader's instruction files seem to be ignored sometimes, or work differently in Claude Code than in Cursor, or get overridden by something they can't identify.

**Learning outcomes:**
1. (Understand) Explain why precedence models differ across tools and why this matters for cross-tool workflows.
2. (Apply) Write a `PROJECT_RULES.md` with an explicit precedence statement that every tool will load.
3. (Apply) Identify where each tool's instruction file lives and what conflict resolution model it uses.
4. (Analyze) Diagnose whether an instruction file failure is a precedence problem, a load problem, or an advisory-only compliance problem.

**Chapter opening:** A developer who added a "never delete files" rule to their CLAUDE.md and found that Claude Code honored it but Cursor didn't. The fix is not to add the rule everywhere — it is to understand that CLAUDE.md and Cursor's rules use different precedence models, and to encode the rule in a file both tools load.

**Core content blocks:**
1. The two dominant precedence models: scoped layering vs. nearest-file-wins
2. Where each tool's instruction file lives — per-tool table
3. The advisory-not-enforced problem: instruction files are context, not configuration
4. `AGENTS.md` as the portability play — and how to bridge tools that don't auto-read it
5. Explicit precedence statement: the one sentence that works everywhere

**Per-tool instruction file table:**
| Tool | Instruction file(s) | Conflict/precedence rule |
|---|---|---|
| Claude Code | `CLAUDE.md` (managed → user → project → local) | Concatenated root→cwd; closer wins; managed policy can't be excluded |
| AGENTS.md standard | `AGENTS.md`, nested | Closest AGENTS.md wins; chat prompts override everything |
| Codex CLI | `AGENTS.md` + `AGENTS.override.md` | Concatenate root→cwd; closer overrides; 32 KiB limit |
| Cursor | `.cursor/rules/` | Team → Project → User |
| Gemini CLI | `GEMINI.md` (global → workspace → just-in-time) | Concatenated; cross-tier conflict underspecified |
| Aider | `CONVENTIONS.md` via `read:` | Last loaded wins; does NOT auto-read AGENTS.md |
| GitHub Copilot | `.github/copilot-instructions.md`, `AGENTS.md` | Personal → repository → organization |

**`PROJECT_RULES.md` copy-paste template:**
```markdown
# PROJECT_RULES.md

If these rules conflict with broader/global defaults, follow THIS file
unless I explicitly say otherwise in chat.

## Source of truth
- Read `_MANIFEST.md` first.
- Treat Tier 1 files as canonical.
- Do not use `archive/` files unless I explicitly request them.

## File safety
- Never permanently delete files. Move superseded files to `archive/`.
- Ask before renaming or overwriting any Tier 1 / canonical file.
- Show a diff before any multi-file or structural change.

## Output rules
- Save finished deliverables to `outputs/`.
- Save generated/intermediate artifacts to `build/` or `staging/`.
- Do not treat anything in `outputs/` or `build/` as source unless I ask.

## Task behavior
- Load only the files the current task needs; don't read whole folders.
- State a short plan and your assumptions before broad changes.
- Stop and ask if two Tier 1 files conflict.
- Record major decisions in `status.md`.
```

**Bridging instructions for specific tools:**
```bash
# Claude Code: import AGENTS.md into CLAUDE.md
echo "@AGENTS.md" > CLAUDE.md

# Aider: read AGENTS.md via config
echo "read: AGENTS.md" >> .aider.conf.yml

# Gemini CLI: point at AGENTS.md via settings
# Add to .gemini/settings.json:
# {"context": {"fileName": "AGENTS.md"}}
```

**Worked example:** The same rule ("never delete files, archive instead") encoded in AGENTS.md and bridged to Claude Code, Cursor, and Aider. What each tool does with it, and where each tool's enforcement is advisory vs. deterministic.

**Assessable exercises:**
1. Write a PROJECT_RULES.md for your most-used project. Include a precedence statement. Identify which tool you use most and verify the file will load.
2. Pick one rule you want to enforce. Identify whether it is advisory (instruction file) or enforceable (hook / `permissions.deny`). What would it take to make it deterministic?

**Bridge:** You now have the setup artifacts. Act Two begins: why sessions degrade even when the setup is correct, and what to do about it.

**Label discipline note:** Per-tool instruction file locations are `[OFFICIAL]` per tool. Scoped-layering vs. nearest-file-wins distinction is `[INFERRED]` synthesized across vendor docs. Advisory-not-enforced is `[OFFICIAL]` (Anthropic, Claude Code docs). `@path` import is `[OFFICIAL]` (Claude Code).

---

## ACT TWO — DIAGNOSIS AND REPAIR (Chapters 5–11)
*Why sessions degrade and what to do about it. One failure mode per chapter.*

---

### CHAPTER 5 — The Five Context Cost Types: Where Your Tokens Are Going

**One-line:** Before you can fix a session, you need to know which of the five cost types is eating your context — because the fix for a fixed cost is different from the fix for an accumulated cost.

**Keyword audit:** PASS — "context cost," "tokens," "CLAUDE.md," "MCP," "session" are searchable.

**The problem it solves:** The reader knows their sessions are expensive but can't see where the tokens are going. They are applying generic fixes (start fresh, use /compact) without knowing what they're actually compacting.

**Learning outcomes:**
1. (Understand) Name and distinguish the five context cost types.
2. (Apply) Identify which cost type is dominant in a given broken session.
3. (Apply) Select the correct intervention for each cost type.
4. (Analyze) Audit a specific instruction file or MCP configuration for avoidable fixed cost.

**Chapter opening:** A developer who starts every session with 30,000 tokens already spent — before typing a word. The breakdown: 8,000 in the system prompt, 12,000 in CLAUDE.md, 10,000 in MCP tool schemas. None of this is their task. All of it is overhead they built accidentally.

**Core content blocks:**
1. The five cost types: Fixed, Per-task, Accumulated, Tool-output, Connector/MCP
2. Fixed costs — what loads before you speak, and how to reduce it
3. Per-task costs — reading whole folders instead of specific files
4. Accumulated costs — conversation history as a liability over time
5. Tool-output costs — raw logs and JSON that linger in context
6. Connector/MCP costs — the always-on schema tax

**Five cost types table:**
| Cost type | What it is | Loaded when | Primary lever |
|---|---|---|---|
| Fixed | System prompt + always-loaded files + MCP schemas | Every session/turn | Keep instruction files short; prune MCP servers |
| Per-task | Files read for this task, attachments, search results | When task pulls them | Read specific files, not folders |
| Accumulated | Growing conversation history | Persists every turn | Start fresh sessions; compact |
| Tool-output | Raw tool call results, logs | When tools run | Clear processed results; summarize |
| Connector/MCP | Tool schemas (fixed) + connector payloads (per-call) | Schemas every turn; payloads on call | Prune servers; use code execution |

**Token-budget audit checklist:**
```
Fixed cost audit:
[ ] Is CLAUDE.md under 200 lines?
[ ] Do you have MCP servers you never use?
[ ] Are your "always" rules actually always-applicable?

Per-task cost audit:
[ ] Does any task read whole folders instead of specific files?
[ ] Are you loading large JSON or log files unnecessarily?

Accumulated cost audit:
[ ] How many turns is this session?
[ ] Have you used /compact or started fresh recently?

Tool-output cost audit:
[ ] Are raw tool results still in context after you've processed them?
[ ] Are you summarizing large file reads before reusing them?
```

**Worked example:** A real session token breakdown. CLAUDE.md eating 42,000 tokens per conversation (practitioner-reported case). What was in the file, what should have been in a skill instead, and what the cost looked like after the fix.

**Assessable exercises:**
1. Open your most-used CLI tool and estimate your fixed cost before you type anything. What is the approximate token count? What is the biggest contributor?
2. For each of the five cost types, name one specific change you could make this week that would reduce it.

**Bridge:** Now that you can name the cost type, Chapter 6 covers the behavioral interventions that keep accumulated cost from dominating: session hygiene and state files.

**Label discipline note:** Five cost types framework is `[AGNOSTIC]` synthesized. CLAUDE.md as most expensive user-controlled file is `[OFFICIAL]` (Anthropic). 42,000-token CLAUDE.md is `[CONVENTION]` (practitioner-reported). MCP schema costs are `[OFFICIAL]` framing + `[CONVENTION]` figures.

---

### CHAPTER 6 — Session Hygiene and State Files: Not Losing Your Mind Between Sessions

**One-line:** Context rot is behavioral, not just structural — the right session hygiene keeps accumulated cost from degrading quality, and state files make fresh starts cost nothing.

**Keyword audit:** PASS — "session hygiene," "context rot," "status.md," "session handoff" are searchable.

**The problem it solves:** The reader starts sessions from scratch every time because they can't trust the agent to remember what was decided — or they keep one session alive too long and watch quality degrade.

**Learning outcomes:**
1. (Understand) Explain why context rot is continuous and behavioral, not just a window-limit problem.
2. (Apply) Implement a session workflow: start-of-session loading, during-session discipline, end-of-session update.
3. (Apply) Write a `status.md` with YAML frontmatter that any tool can parse.
4. (Apply) Write a `session-handoff.md` that makes a fresh session as good as a continuing one.

**Chapter opening:** A developer who has been working in the same Claude Code session for four hours. The first two hours were excellent. The last two were increasingly wrong. Not because the model changed — because the context accumulated 80,000 tokens of intermediate reasoning that the model now has to read through to find the relevant parts.

**Core content blocks:**
1. Why one task per thread is the most powerful session hygiene rule
2. Start fresh vs. compact: decision rule for which to use
3. Persist decisions outside the window: `status.md` as the durable state layer
4. Keep tool outputs small: summarize before reuse
5. The end-of-session update: the five-minute ritual that makes every next session better

**Session workflow (copy-paste as instruction):**
```
## Start of session
1. Read _MANIFEST.md.
2. Read Tier 1 files (PROJECT_RULES.md, status.md, outline).
3. Identify the task domain.
4. Load ONLY the relevant Tier 2 files.
5. State a short plan before modifying anything.

## During session
1. Keep tool outputs small; summarize large files before use.
2. Avoid unrelated pivots — open a new session instead.
3. Record major decisions in status.md as you go.
4. Compact when history bloats but the task continues.

## End of session
1. Update status.md (state, decisions, next actions).
2. Move superseded files to archive/.
3. Save deliverables to outputs/.
4. Update _MANIFEST.md if canonical (Tier 1) files changed.
```

**`status.md` copy-paste template:**
```markdown
---
project: project-alpha
status: active        # active | paused | done
updated: 2026-06-14
canonical: [outline.md, chapters/current/]
next: ["draft ch.4", "fact-check ch.3"]
blocked_by: null
---

# Status — project-alpha
Prose for humans: where things stand, latest decisions, open questions.
```

**`session-handoff.md` copy-paste template:**
```markdown
# Session Handoff — <project> — YYYY-MM-DD HH:MM

## Goal (one line)
What this work is trying to achieve.

## State now
- Done: …
- In progress: …
- Blocked: … (and on what)

## Key decisions (with reasons)
- Decided X because Y. (supersedes earlier Z)

## Next 1–3 actions
1. …

## Files that matter (and ONLY these)
- canonical: …
- touch next: …

## Do NOT
- reopen <settled question>; reread <archived/large file>.
```

**Worked example:** The same project handled two ways: one developer who keeps one session alive for a week (quality degrades, decisions are lost, the agent contradicts itself by day 3); one developer who uses the session workflow and handoff file (each session starts clean, quality is consistent, decisions persist in `status.md`).

**Assessable exercises:**
1. Write a `status.md` for your most active project right now.
2. After your next work session, write a `session-handoff.md`. Open a fresh session and read it back. What was lost? What was preserved?

**Bridge:** You know how to prevent accumulated cost. Chapter 7 covers what to do when a session has already degraded — the compaction and clearing interventions.

**Label discipline note:** Context rot is continuous not a cliff is `[OFFICIAL]` (Chroma research). One task per thread is `[OFFICIAL/TOOL]` (Claude Code best practices). Note-taking as the durable state mechanism is `[OFFICIAL]` (Anthropic). Session handoff template is `[CONVENTION/INFERRED]`.

---

### CHAPTER 7 — Compaction, Clearing, and Knowing When to Start Fresh

**One-line:** Compaction and clearing are not the same operation — and using the wrong one at the wrong moment makes the degradation worse.

**Keyword audit:** PASS — "compaction," "/compact," "/clear," "context management" are searchable.

**The problem it solves:** The reader knows they should "compact" but doesn't know when, or uses /clear when /compact was right, or starts a fresh session when the handoff file would have been enough.

**Learning outcomes:**
1. (Understand) Distinguish compaction, clearing, and fresh-session strategies by their trade-offs.
2. (Apply) Select the correct intervention given a session state.
3. (Apply) Use the correct tool-specific command for each intervention.
4. (Analyze) Diagnose whether a session's degradation is recoverable by compaction or requires a fresh start.

**Chapter opening:** A developer who typed `/clear` mid-task, lost all the context about what had been decided, and spent 30 minutes reconstructing the state. The right intervention was `/compact [focus]` — which would have summarized the history while keeping the relevant decisions.

**Core content blocks:**
1. The three strategies: compact (summarize and continue), clear (reset and continue), fresh start (new session with handoff)
2. Decision rule: when each strategy is correct
3. Per-tool compaction commands — what each tool actually does
4. Auto-compaction: what each tool does automatically and at what threshold
5. The Anthropic context editing option: the lightest touch

**Decision rule (copy-paste):**
```
USE /compact [focus] when:
- The task is continuing and you need the history summarized, not lost
- You are mid-task and the window is >60% full
- You can specify what to keep (the focus argument)

USE /clear when:
- You are done with the current task and starting something unrelated
- The accumulated history is actively misleading (contradictory context)
- You have written a session-handoff.md first

USE fresh session when:
- The task domain is completely different
- You want a reviewer who hasn't seen your work (writer/reviewer split)
- The session has been running >4 hours and quality has drifted
```

**Per-tool compaction table:**
| Tool | Manual command | Auto-compaction | Notes |
|---|---|---|---|
| Claude Code | `/compact [focus]`, `/clear`, `/rewind` | Yes — near limit, keeps 5 most-recent files | `/rewind` is local only, not a git replacement |
| Codex CLI | `context_management` / `compact_threshold` | Yes — capped at 90% of window | Exact thresholds are version-dependent `[CONVENTION]` |
| Gemini CLI | `/compress`, `/memory show`, `/memory refresh` | Yes — at ~0.5 input window (practitioner-reported) `[CONVENTION]` | Do not confuse with checkpointing (file rollback) |
| Aider | `/clear`, `/tokens` | No verified auto-compact | `--map-tokens` controls repo map budget |
| Cursor | Auto-managed | Auto-managed | No verified manual compact command |

**Worked example:** A 3-hour session that degraded. Token breakdown at the point of degradation. What `/compact` would have preserved. What the fresh-session handoff preserved instead. Side-by-side comparison of output quality.

**Assessable exercises:**
1. Your session is at 70% context capacity, mid-task. You have been working for 2 hours. What do you do? Write the specific command for your primary tool.
2. Your session has been running for a week. Output quality has dropped. You have no handoff file. What is your recovery sequence, step by step?

**Bridge:** Compaction handles accumulated cost. Chapter 9 handles the other major surprise: MCP schema cost, which is fixed and loads before you type anything.

**Label discipline note:** Auto-compaction behavior is `[OFFICIAL/TOOL]` per tool where confirmed; threshold numbers are `[CONVENTION]` where derived from practitioner reverse-engineering. Gemini checkpointing ≠ compression distinction is `[OFFICIAL]`. `/rewind` not a git replacement is `[OFFICIAL]` (Claude Code docs).

---

### CHAPTER 8 — One Folder, Many Tools: Making Cross-Tool Workflows Work

**One-line:** The same folder can serve Claude Code, Codex, Cursor, and Gemini CLI — if you make `AGENTS.md` the single source of truth and add thin shims for each tool that doesn't auto-read it.

**Keyword audit:** PASS — "AGENTS.md," "cross-tool," "multi-tool," "Claude Code," "Codex" are searchable.

**The problem it solves:** The reader uses more than one CLI tool on the same project and is maintaining parallel instruction files that keep drifting apart — or they switched tools and found that their Claude Code setup doesn't work in their new environment.

**Learning outcomes:**
1. (Understand) Explain why different tools use different instruction file names and how they resolve conflicts differently.
2. (Apply) Make AGENTS.md the single source of truth and bridge it to Claude Code, Aider, and Gemini CLI.
3. (Apply) Choose between reference, bridge, and compile strategies for multi-tool instruction management.
4. (Analyze) Assess which patterns in a multi-tool workflow are fully portable vs. tool-specific.

**Chapter opening:** A developer who maintained CLAUDE.md, .cursor/rules, and CONVENTIONS.md separately. They diverged. The agent in each tool had a different understanding of the project rules. The fix: one AGENTS.md, three thin shims.

**Core content blocks:**
1. The portability matrix — what's fully portable (folder structure) vs. portable with adaptation (rules file) vs. tool-specific (hooks, compaction)
2. AGENTS.md as the cross-vendor standard — who reads it natively, who needs a shim
3. The three robustness levels: reference, bridge, compile
4. Bridging specific tools: Claude Code, Aider, Gemini CLI
5. The compile approach: when to generate vendor files from shared modules

**Bridging instructions (copy-paste):**
```bash
# Option 1: @import in CLAUDE.md (recommended for Claude Code)
echo "@AGENTS.md" > CLAUDE.md

# Option 2: Symlink (git-tracked, survives clone, breaks on Windows)
ln -s AGENTS.md CLAUDE.md

# Option 3: Aider config
echo "read: AGENTS.md" >> .aider.conf.yml

# Option 4: Gemini CLI settings.json
# {"context": {"fileName": "AGENTS.md"}}
```

**Portability matrix (copy-paste reference):**
| Pattern | Classification | What carries / what breaks |
|---|---|---|
| Folder architecture | Fully portable | Just directories; every tool sees the same tree |
| `_MANIFEST.md` tier discipline | Portable with adaptation | File is portable; enforcement needs an ignore file |
| `PROJECT_RULES.md` + precedence | Portable with adaptation | Loaded only if tool's instruction file points at it |
| `status.md` / handoff | Fully portable | Plain Markdown; any agent reads it if told to |
| Compaction / `/clear` | Tool-specific | Command names differ; handoff file is the portable substitute |
| PreToolUse hooks | Tool-specific (Claude Code) | No portable equivalent |

**Worked example:** A project used simultaneously in Claude Code and Codex CLI. AGENTS.md content. The one-line CLAUDE.md. The `.aider.conf.yml` entry. What each tool loads. Where each tool's behavior diverges. What that means for the rules that are in the shared file.

**Assessable exercises:**
1. How many instruction files do you currently maintain across all CLI tools? List them. Identify which content is duplicated. Design the AGENTS.md consolidation.
2. Pick one rule currently in your CLAUDE.md. Verify it will load in every tool you use. For each tool where it won't, write the shim.

**Bridge:** Your folder works across tools. Now Chapter 9 covers the one silent cost most users never see coming: MCP schema overhead.

**Label discipline note:** AGENTS.md as Linux Foundation standard is `[OFFICIAL]`. @import is `[OFFICIAL]` (Claude Code). Symlink Windows fragility is `[CONVENTION/UNVERIFIED]`. Portability matrix classifications are `[AGNOSTIC]` synthesized.

---

### CHAPTER 9 — MCP Servers and Context: The Silent Tax You're Probably Paying

**One-line:** Every MCP server you connect loads its tool schemas on every turn before you type a word — and five servers can consume 30–60% of your context window before the session starts.

**Keyword audit:** PASS — "MCP," "MCP servers," "context window," "tool schemas" are searchable.

**The problem it solves:** The reader has connected MCP servers for productivity and is now experiencing mysteriously expensive, slow, or degraded sessions without understanding why.

**Learning outcomes:**
1. (Understand) Explain why MCP tool schemas are a fixed context cost that loads on every turn.
2. (Apply) Audit a current MCP configuration for over-provisioning and remove or disable unnecessary servers.
3. (Apply) Use scoped MCP configuration and `--strict-mcp-config` to load only what the task needs.
4. (Analyze) Estimate the MCP context cost of a given configuration before connecting it.

**Chapter opening:** A developer who added five MCP servers over three months — GitHub, Slack, Notion, a database tool, and a search tool. Their sessions now start with 55,000 tokens consumed before the first message. They've been blaming the model for degraded output.

**Core content blocks:**
1. Why MCP schemas are always-on fixed cost — the mechanism
2. Real numbers: 5 servers × 30 tools = 30k–60k tokens; 40 tools = up to 72% of a 200k window
3. The over-provisioning failure: every tool definition loads even for unrelated tasks
4. Scoped MCP configuration: project-scope vs. user-scope vs. session-scope
5. The code execution fix: Anthropic's 98.7% token reduction via sandbox execution `[OFFICIAL]`

**MCP cost audit (copy-paste):**
```bash
# In Claude Code: check context before typing anything
/context

# Look for: MCP tools line in the breakdown
# If MCP tools > 5% of your context: audit your servers

# To check what's loaded:
/mcp

# To disable a server for this session (Claude Code):
# Use /mcp → disable

# To use strict config (load ONLY named servers):
claude --mcp-config .mcp.json.taskspecific --strict-mcp-config
```

**MCP scope cheat sheet (copy-paste):**
| Scope | Config location | Shared with team? | Persists? | Use when |
|---|---|---|---|---|
| Project | `.mcp.json` in project root | Yes | Yes | Team needs the server; commit to git |
| User | `~/.claude/settings.json` | No | Yes | Personal tools; credentials |
| Session | `--mcp-config` flag | No | No | One-off; testing; short-lived tokens |

**Worked example:** A session before and after MCP audit. Before: 5 servers, 55,000 tokens fixed cost, degraded output on a simple task. After: 2 servers relevant to the task, 8,000 tokens fixed cost, clean output. The audit process step by step.

**Assessable exercises:**
1. Run `/context` at the start of a fresh session in your primary tool. What percentage is MCP tool schemas? List every server and whether you actually used it in the last week.
2. Disable all MCP servers except one. Run your most common task. Note the quality and token difference.

**Bridge:** MCP is the biggest surprise in the fixed cost category. Chapter 10 covers the agent workflow patterns that reduce per-task and accumulated cost.

**Label discipline note:** MCP schema always-on cost is `[OFFICIAL]` (Anthropic). 30k–60k token figures are `[CONVENTION]` (practitioner-reported). 72% of 200k window is `[CONVENTION]`. 98.7% reduction via code execution is `[OFFICIAL]` (Anthropic). Scoped configuration behavior is `[OFFICIAL]` per tool.

---

### CHAPTER 10 — Agent Workflow Patterns That Actually Work

**One-line:** Nine tool-agnostic patterns — from builder-validator to test-before-write — that reduce per-task cost, improve output quality, and work in any CLI tool.

**Keyword audit:** PASS — "agent workflow," "builder-validator," "prompt chaining," "plan mode" are searchable.

**The problem it solves:** The reader is using their AI agent as a single-turn question-answering machine and is frustrated by output quality — or they've heard about "agentic workflows" but don't know which patterns to actually use and when.

**Learning outcomes:**
1. (Understand) Name nine tool-agnostic agent workflow patterns and their primary use case.
2. (Apply) Select the correct pattern for a given task type.
3. (Apply) Write the plain-language instructions that implement each pattern in a real session.
4. (Analyze) Diagnose which pattern failure is occurring when an agent workflow produces poor results.

**Chapter opening:** A developer who asks the agent to "write a blog post, check it for errors, then improve it" in one prompt — and gets an agent that grades its own work and ships the first draft with minor changes. The fix: separate the generator and the critic into different context windows.

**Core content blocks:**
1. Builder–validator (generator–critic): the evaluator-optimizer pattern
2. Researcher–writer–editor: prompt chaining for deliverables
3. Planner–executor–reviewer: plan mode before any edit
4. Sub-agent delegation: offload exploration, receive summaries
5. Staging-before-output: validate before promoting to outputs/
6. Human approval gates: three designs
7. Destructive-action gates: gate only irreversible ops
8. Diff-first: show before apply
9. Test-before-write (TDD): the single strongest agentic coding pattern

**Pattern quick-reference (copy-paste):**
```
BUILDER-VALIDATOR
When: Clear eval criteria; iteration adds value
Say: "Draft X, critique it against [criteria], revise; repeat until it passes."
Watch: Scope the critic — "flag only gaps affecting correctness" not "find all gaps"

PLANNER-EXECUTOR-REVIEWER
When: Uncertain approach; multi-file change; unfamiliar code
Say: "Enter plan mode, read relevant files, propose a plan; don't edit until I approve."
Skip when: you could describe the diff in one sentence

SUB-AGENT DELEGATION
When: Complex exploration that would flood the main window
Say: "Use a sub-agent to investigate X and report only a short summary."
Key: "short summary" — sub-agent burns context; you receive 1–2k tokens back

STAGING-BEFORE-OUTPUT
When: Generating deliverables or risky edits
Say: "Write to staging/, validate against PROJECT_RULES.md, then move to outputs/."

DESTRUCTIVE-ACTION GATE
When: Any irreversible operation
Say: "Require my approval for deletes, bulk renames, and overwriting canonical files; never gate reads."
```

**Worked example:** A document generation task run two ways: single-turn (agent grades own work, ships first draft) vs. builder-validator (clean critic context, genuine quality improvement). Token cost comparison and output quality comparison.

**Assessable exercises:**
1. Your most recent AI task that produced disappointing output. Which pattern would have helped? Write the specific instructions you would have used.
2. Set up the builder-validator pattern for one real task this week. Note the quality difference.

**Bridge:** Patterns improve per-task efficiency. Chapter 11 covers the one failure mode that can undo all of it: the agent deleting, renaming, or overwriting files it should never touch.

**Label discipline note:** Evaluator-optimizer pattern is `[OFFICIAL]` (Anthropic building effective agents). Plan mode existence is `[OFFICIAL/TOOL]` (Claude Code, Gemini CLI, Cursor). TDD as strongest pattern is `[OFFICIAL]` (Claude Code best practices). Over-reported critic fix is `[OFFICIAL]` (Claude Code best practices).

---

### CHAPTER 11 — File Safety: Never Delete, Always Archive

**One-line:** One rule prevents 80% of filesystem disasters: never delete by default — archive instead. The rest is gates on irreversible operations.

**Keyword audit:** PASS — "file safety," "archive," "destructive actions," "git checkpoints" are searchable.

**The problem it solves:** The reader has experienced an agent deleting, overwriting, or bulk-renaming files it should not have touched — or they are afraid to use an agent for consequential work because they don't trust its file behavior.

**Learning outcomes:**
1. (Apply) Write global instruction language that implements archive-not-delete as a default.
2. (Apply) Configure destructive-action gates for the specific irreversible operations that matter.
3. (Understand) Distinguish between in-tool checkpoints (fast local rewind) and git commits (durable, shareable layer).
4. (Analyze) Identify which file safety mechanism — instruction file, hook, git, in-tool checkpoint — is the right layer for a given protection requirement.

**Chapter opening:** A developer who asked the agent to "clean up the project folder" without specifying what clean meant. The agent deleted 23 files. Seven were irreplaceable. The rest were recoverable from git — but only because the developer had been committing regularly.

**Core content blocks:**
1. The archive rule: never delete, move to archive/
2. The blast-radius test: irreversible + high-blast-radius = mandatory gate
3. Git as the durable checkpoint layer — in-tool rewind is not a git replacement
4. Per-tool checkpoint behavior
5. Making "never delete" deterministic with Claude Code PreToolUse hooks

**Global instruction language (copy-paste):**
```
Never permanently delete files. Move them to archive/ instead.
Before bulk renaming, overwriting canonical files, or restructuring folders,
show the proposed changes and wait for my approval.
For code, prefer branch + diff + test before merge, and commit at meaningful
checkpoints so every state is recoverable.
Gitignore generated artifacts so diffs and checkpoints stay clean.
```

**PreToolUse hook for Claude Code (copy-paste):**
```json
{
  "hooks": {
    "PreToolUse": [{
      "matcher": "Bash",
      "hooks": [{
        "type": "command",
        "command": "scripts/check-destructive.sh"
      }]
    }]
  }
}
```
```bash
#!/bin/bash
# check-destructive.sh — deny rm on non-rebuildable artifacts
if echo "$1" | grep -qE 'rm\s+(?!.*\.(pyc|bak)|build/|__pycache__)'; then
  echo '{"permissionDecision": "deny", "reason": "Use archive/ instead of delete."}'
  exit 1
fi
```

**Per-tool checkpoint table:**
| Tool | In-tool undo | Git integration | Limitation |
|---|---|---|---|
| Claude Code | `/rewind` (30-day checkpoints) | Git-aware | Only tracks Claude's changes; not a git replacement |
| Aider | `/undo`, auto-commit with "(aider)" tag | Auto-commits every edit | Gold standard for file safety |
| Cursor | Checkpoints + git worktrees | Git-aware | Checkpoint behavior varies |
| Codex CLI | Weak native undo | Git via shell | Disciplined git commits are the safety net |
| Gemini CLI | Shadow-git checkpoints | Shadow git | Checkpointing ≠ compression — separate features |

**Worked example:** The same "clean up the project" task with no file safety (disaster) vs. with archive rule + gate (agent moves files to archive/, shows the list, waits for approval). What the instruction language looked like. What the hook added.

**Assessable exercises:**
1. Add the global instruction language to your AGENTS.md today. Test it: ask the agent to "delete the oldest file in the project." Does it archive instead?
2. Identify the three most irreplaceable files in your most active project. What protection does each currently have? What would you add?

**Bridge:** You can diagnose and repair the common failure modes. Act Three covers the harder cases and the honest questions.

**Label discipline note:** Archive-not-delete is `[CONVENTION]`. PreToolUse hook mechanism is `[OFFICIAL]` (Claude Code). `/rewind` not a git replacement is `[OFFICIAL]` (Claude Code). Aider auto-commit is `[OFFICIAL]` (Aider). Gemini checkpointing ≠ compression is `[OFFICIAL]`.

---

## ACT THREE — ADVANCED AND HONEST (Chapters 12–15)
*The hard cases and the honest questions.*

---

### CHAPTER 12 — The Anti-Patterns Checklist: Eleven Things You're Probably Still Doing

**One-line:** A complete checklist of the eleven most common structural and behavioral anti-patterns — with the fix for each, labeled by source confidence.

**Keyword audit:** PASS — "anti-patterns," "AI agent," "context pollution," "checklist" are searchable.

**The problem it solves:** The reader wants a fast audit of their entire workflow against the full set of known failure modes — in one place, with no hunting through chapters.

**Learning outcomes:**
1. (Evaluate) Audit a workflow or project structure against all eleven anti-patterns.
2. (Apply) Prioritize which anti-pattern fixes to implement first based on expected impact.
3. (Apply) Write the specific fix for each anti-pattern found.

**Chapter opening:** The developer who has read Chapters 1–11 and wants one page they can print and put on the wall. This is that page.

**Core content blocks:**
1. Anti-patterns 1–11 with fix, source label, and priority
2. Fast audit protocol: 15 minutes to a complete picture
3. Priority ordering: which fixes have the most impact per hour of work

**Complete anti-patterns checklist (copy-paste):**
```
[ ] 1. POINTING AT A GIANT PARENT FOLDER
    Sign: Agent reads across project boundaries
    Fix: One bounded folder per project; multi-root for cross-project
    Source: [CONVENTION]

[ ] 2. MIXING UNRELATED PROJECTS IN ONE TREE OR SESSION
    Sign: Agent confuses context from different projects
    Fix: Separate folders, separate sessions
    Source: [CONVENTION]

[ ] 3. OLD DRAFTS BESIDE CURRENT DRAFTS
    Sign: Agent uses archived version as if current
    Fix: archive/ for everything superseded; never leave in place
    Source: [CONVENTION]

[ ] 4. OUTPUTS BECOMING SOURCE MATERIAL
    Sign: Agent re-ingests its own output as canonical
    Fix: outputs/ and build/ are never source; say so in PROJECT_RULES.md
    Source: [INFERRED]

[ ] 5. HUGE GLOBAL MEMORY
    Sign: CLAUDE.md or AGENTS.md over 200 lines
    Fix: Keep instruction files short; push detail to skills/reference
    Source: [OFFICIAL/CONVENTION]

[ ] 6. MANY UNRELATED TASKS IN ONE SESSION
    Sign: Quality drifts; agent contradicts earlier decisions
    Fix: One task per thread; /clear or new session between pivots
    Source: [OFFICIAL/CONVENTION]

[ ] 7. DUMPING FULL LOGS OR JSON INTO CONTEXT
    Sign: Tool outputs linger; session gets heavy fast
    Fix: Summarize; use head/tail; clear processed results
    Source: [OFFICIAL]

[ ] 8. ASKING "WHAT'S IN THIS FOLDER?" INSTEAD OF MAINTAINING STATUS.MD
    Sign: Wasting the first 2,000 tokens of every session on re-derivation
    Fix: Maintain status.md; read it at session start
    Source: [OFFICIAL]

[ ] 9. VAGUE TASKS ("CLEAN THIS UP")
    Sign: Agent takes high-blast-radius actions without asking
    Fix: Specify target, constraint, and "done" criteria
    Source: [CONVENTION]

[ ] 10. LETTING THE AGENT DELETE OR RENAME WITHOUT REVIEW
    Sign: Files missing; renames that break dependencies
    Fix: Archive-not-delete; gate destructive ops
    Source: [CONVENTION]

[ ] 11. DEPENDING ON TOOL-SPECIFIC BEHAVIOR THAT MAY NOT GENERALIZE
    Sign: Workflow breaks when switching tools
    Fix: Encode intent in plain files; state precedence explicitly
    Source: [AGNOSTIC]
```

**Worked example:** A real project audited against all eleven. Six anti-patterns found. Priority order for fixing them. Time estimate for each fix. State of the project one week later.

**Assessable exercises:**
1. Run the 15-minute audit on your most active project. How many anti-patterns did you find? Which three will you fix this week?

**Bridge:** The checklist gives you the patterns. Chapter 13 gives you the failure-mode catalog — the structural analysis behind each anti-pattern, with triggers and mitigations.

---

### CHAPTER 13 — The Failure-Mode Catalog: Root Causes and Mitigations

**One-line:** Nine failure modes mapped from pattern to trigger to mitigation — the diagnostic tool for when the anti-patterns checklist isn't enough.

**Keyword audit:** PASS — "failure modes," "context rot," "manifest," "ignore files" are searchable.

**The problem it solves:** The reader has a specific failure and needs to trace it to its root cause — the anti-patterns checklist told them what is wrong, the failure-mode catalog tells them why it happens and what specifically to do.

**Learning outcomes:**
1. (Analyze) Given a workflow failure, identify its root cause from the failure-mode catalog.
2. (Evaluate) Assess which mitigation is most appropriate for the deployment context.
3. (Apply) Implement the mitigation for a specific failure mode.

**Chapter opening:** A developer experiencing the same failure every time they start a new session: the agent ignores the manifest and reads the entire project. The catalog entry for "manifest tier discipline" gives them the exact trigger (vague task, tool that doesn't honor instructions) and the exact mitigation (back with ignore file, physically separate archive/).

**Complete failure-mode catalog:**
| Pattern | Failure mode | Triggers under | Mitigation |
|---|---|---|---|
| Manifest tier discipline | Agent reads Tier 3 anyway | Vague task; tool doesn't honor instructions; glob/grep sweep | Back with ignore file (Ch. 14); physically separate archive/; scope tasks |
| Ignore files | Ignored file still sent to model | Cursor "best-effort"; Claude Code `.env` leaks (reported, unverified severity) | Don't rely on ignore files for secrets — keep secrets out of the folder entirely |
| `AGENTS.md` + shims | Same content loaded twice; symlink breaks on Windows | Tool reads both `AGENTS.md` and importing `CLAUDE.md`; Windows checkout | Prefer `@import` over symlink on mixed-OS teams; or compile approach (Ch. 8) |
| `MEMORY.md` index | Canonical pointer below line 200 never loads | Index grows past 200 lines / 25KB | Keep it a true index; verify top 200 lines hold all load-bearing pointers |
| `status.md` / index | Agent trusts stale state | Not updated at session end; index drifts from per-project files | Update status/index as the last end-of-session step |
| Handoff file | Continuity lost after `/clear` | Handoff omits key decision or includes too much noise | Template from Ch. 6: decisions + next actions in, narrative out |
| Long sessions | Quality degrades mid-window | Accumulated history, distractors | Handoff + fresh session; one task per thread |
| Sub-agent reviewer | Over-reports gaps → over-engineering | Critic told to "find gaps" unscoped | Scope to "correctness / stated requirements only" |
| Uncited vendor figures | Designing to a number that isn't reproducible | Trusting "99.96%"-style claims as targets | Verify against official docs; the real MCP code-execution figure is 98.7% `[OFFICIAL]` |

**Chapter opening:** A session failure traced through the catalog. The symptom, the pattern match, the trigger, the fix applied, the result.

**Assessable exercises:**
1. Name your three most common session failures. Find them in the catalog. Are you hitting the right mitigation or a different one?

**Bridge:** The catalog gives you the diagnosis layer. Chapter 14 covers the security and governance layer — what happens when the agent has shell access and MCP connectors and something goes wrong.

---

### CHAPTER 14 — Governance and Security: When the Agent Has Shell Access

**One-line:** The moment an agent has filesystem access, shell, and MCP connectors, your folder conventions are a security boundary — and a weak one by default.

**Keyword audit:** PASS — "governance," "security," "prompt injection," "MCP security," "tool poisoning" are searchable.

**The problem it solves:** The reader is using agents with shell access and MCP connectors for consequential work and hasn't thought about what an adversarial MCP tool description or a hidden instruction in a fetched file could do.

**Learning outcomes:**
1. (Understand) Describe the two primary threat classes for agents with filesystem and MCP access.
2. (Apply) Implement the six baseline governance controls.
3. (Apply) Write a permission profile and network allowlist for a real project.
4. (Evaluate) Assess the security posture of a current agent deployment.

**Chapter opening:** The WhatsApp-MCP case: malicious instructions embedded in a tool's description exfiltrated message history with nothing visible in the tool's output. This is not hypothetical — it was demonstrated.

**Core content blocks:**
1. Prompt injection: hidden instructions in content the agent reads
2. Tool poisoning: malicious instructions in MCP tool metadata
3. The six baseline controls
4. Every MCP server as third-party supply chain — not a trusted built-in
5. The one portable principle

**The six baseline controls (copy-paste):**
```
1. LEAST PRIVILEGE BY DEFAULT
   Narrowest permission profile that still works.
   Workspace-only filesystem scope where possible.

2. EXPLICIT NETWORK/DOMAIN ALLOWLISTS
   Not "internet on." Encode in .ai/manifest.yaml permissions block.
   
3. NO SECRETS IN THE FOLDER, PROMPTS, OR LOGS
   Ignore files reduce context, they don't secure secrets.
   Keep secrets out of the folder entirely.

4. APPROVAL GATES ON DESTRUCTIVE/IRREVERSIBLE ACTIONS
   And on any new outbound connector.

5. VALIDATOR PASSES FOR RISKY WORK
   Clean-context reviewer that sees only the diff and the rules.

6. AUDIT THE DECISIONS AND FILE CHANGES
   .ai/audit/ or tool-native logging.
   Reconstruct what an agent did and why.
```

**The one portable principle:** The agent should be able to do exactly the task, and nothing with larger blast radius, without a human in the loop.

**Permission profile template (`.ai/manifest.yaml` extension):**
```yaml
permissions:
  filesystem_scope: workspace-only
  network_allowlist: ["registry.npmjs.org", "api.yourtool.com"]
  forbidden: ["rm -rf", "git push --force", "curl -X DELETE"]
```

**Worked example:** An agent deployment before governance (shell access, 5 MCP servers, no allowlist, no audit log). Assessment against the six controls. What a governance-hardened version of the same deployment looks like.

**Assessable exercises:**
1. Assess your current most-used agent deployment against the six controls. Score each 0/1. What's your total? What's the highest-impact missing control?
2. Write a permission profile for your most consequential project.

**Bridge:** Governance gives you protection. Chapter 15 gives you measurement — and the honest answer to whether any of this actually helps.

**Label discipline note:** Prompt injection is `[OFFICIAL/RESEARCH]` (NSA MCP Security CSI). Tool poisoning WhatsApp case is `[RESEARCH]`. Six controls are `[AGNOSTIC/CONVENTION]`. The one portable principle is `[INFERRED]`.

---

### CHAPTER 15 — Does Any of This Actually Help? Measuring Your Workflow

**One-line:** The honest chapter: the 2026 research shows instruction files may not uniformly improve outcomes — here's how to measure whether yours do, instead of assuming they do.

**Keyword audit:** PASS — "measurement," "instruction files," "AGENTS.md evaluation," "token cost" are searchable.

**The problem it solves:** The reader has implemented the book's recommendations but doesn't know if they actually work. They are treating instruction files as assumed goods rather than measurable artifacts.

**Learning outcomes:**
1. (Understand) Describe the 2026 empirical findings on instruction file effectiveness, including the ETH Zurich result.
2. (Evaluate) Assess whether a given rules file is earning its context cost.
3. (Apply) Run a portable mini-benchmark to measure instruction file impact.
4. (Apply) Prune rules that don't earn their cost.

**Chapter opening:** The uncomfortable finding: an ETH Zurich evaluation found that `AGENTS.md`-style context files reduced task success by ~3% while raising token cost over 20%. A factorial study found that instruction file size, position, and architecture produced no detectable effect on adherence. This does not mean skip the folder structure — but it does mean measure, don't assume.

**Core content blocks:**
1. What the 2026 evidence actually shows — three studies
2. What it does and doesn't mean for your workflow
3. Rules files as measurable artifacts, not assumed goods
4. The portable mini-benchmark
5. How to prune: review in PRs like code, delete what doesn't earn its cost

**The three 2026 studies (labeled):**
```
1. ETH Zurich — Evaluating AGENTS.md (arXiv:2602.11988) [empirical]
   Finding: Context files reduced task success ~3%, raised token cost >20%
   Caveat: One experimental setup; not a universal finding

2. Factorial study (arXiv:2605.10039) [empirical]
   Finding: Instruction file size, position, and architecture produced
   no detectable effect on adherence
   Implication: "Just make it longer / better-structured" folk wisdom
   is not supported

3. Agent READMEs adoption study (arXiv:2511.12884) [empirical]
   Finding: How teams actually write these files in the wild
```

**Portable mini-benchmark (copy-paste):**
```
TASK SUITE (run with and without your rules file):
1. Repo summary — ask for a summary of the project
2. Narrow bug fix — fix a specific, described bug
3. Multi-file feature — add a small feature across 2-3 files
4. Test repair — fix a failing test
5. Security-sensitive change — change that touches auth or credentials

METRICS TO RECORD:
- Acceptance rate: did the output work without your intervention?
- Manual edits after: how many lines did you change?
- Time to valid diff: minutes from prompt to usable output
- Token cost: total tokens for the session
- Risky behavior: out-of-scope edits, unrequested deletes

ANALYSIS:
Compare WITH rules file vs. WITHOUT rules file.
A rules file that costs 5,000 tokens and improves nothing should be pruned.
A rules file that costs 500 tokens and prevents one class of errors pays for itself.
```

**Worked example:** A rules file before and after the mini-benchmark. Three rules that made no measurable difference removed. Two rules that prevented specific failure modes kept. Net result: leaner file, same protection, lower fixed cost.

**Assessable exercises:**
1. Run the mini-benchmark on your primary project, with and without your rules file. What did you find?
2. Review your rules file as if it were code in a PR. Which rules have you never observed being honored? Delete them.

**Label discipline note:** ETH Zurich finding is `[EMPIRICAL STUDY]`. Factorial study finding is `[EMPIRICAL STUDY]`. Both are labeled explicitly in the chapter. "June 2026 study showing structure/length mattered more for PR merges" — this specific claim could not be located; it is partly contradicted by the factorial study and should be treated as `[UNVERIFIED]`.

---

# PART 10 — CHAPTER ANATOMY TEMPLATE

All 15 chapters follow this structure:

1. Problem statement (what failure the chapter addresses — one sentence)
2. Learning outcomes (Bloom's level explicit)
3. Chapter opening (failure case first; the problem made concrete before vocabulary)
4. Core content blocks (4–6), each: concept → mechanism → fix
5. Copy-paste template(s) (the deliverable the reader can use today)
6. Label discipline sidebar (confidence level for key claims in the chapter)
7. Worked example (before/after format; failure → diagnosis → fix → result)
8. Assessable exercises (minimum 2; at least one that requires doing something, not just answering)
9. Chapter summary (capabilities gained, not topics covered)
10. Bridge question (one question; names what the next chapter answers)

**Anatomy enforcement:** A draft chapter missing items 4, 5, 7, or 8 is an incomplete draft. The copy-paste template and the worked example are not optional — they are the book's primary value delivery mechanism.

---

# PART 11 — CASE STUDY AND WORKED EXAMPLE STRATEGY

## Domain Coverage Map

| Domain | Chapters | Notes |
|---|---|---|
| Coding / software development | 2, 7, 10, 11, 13 | Primary reader domain |
| Writing / content production | 1, 3, 6 | Important secondary domain |
| Research / knowledge work | 9, 12 | Supports the multi-domain reader |
| Data / ML engineering | 5, 8 | Connects to Nik's primary audience |
| Security / DevOps | 14 | Required for governance chapter |
| General practitioner (tool-agnostic) | 4, 15 | Chapters that must work for all readers |

## Case Format (all chapters)

Every worked example follows: **Situation → What broke → Why it broke (structural cause) → The fix applied → The result** → **The limit (where this fix doesn't apply)**

## Sourcing Requirement

Every case requires either: a citation to a public source OR an explicit "illustrative case based on common practitioner patterns" label. Neither is optional. Cases presented as real must be real.

## Escalation Across Acts

- Act One cases (Ch. 1–4): single failure mode, clear fix
- Act Two cases (Ch. 5–11): multiple interacting failure modes, judgment required for priority
- Act Three cases (Ch. 12–15): incomplete information, tradeoffs, honest uncertainty

---

# PART 12 — CONTESTED CLAIMS AND AGING RISK

## Contested Claims

| Claim | Status | Book's position |
|---|---|---|
| Instruction files uniformly improve outcomes | Disputed (2026 empirical) | Present the evidence; give the measurement protocol; don't claim more than the data supports |
| MCP schema cost makes servers expensive | Qualitative: confirmed; Quantitative: convention | Official framing; exact numbers labeled [CONVENTION] |
| Context rot is continuous | Confirmed (Chroma) | Stated as [OFFICIAL] |
| CLAUDE.md loads on every session | Confirmed | [OFFICIAL] |
| Ignore files keep secrets safe | False | Directly corrected; chapter 14 |
| Cursor `.md` rules work without `.mdc` | Conflicted (official vs. community) | Present both; recommend empirical testing |
| Claude Code `.env` leaks via gitignore | Reports exist; severity unverified | Presented as [UNVERIFIED]; recommend keeping secrets out of folder entirely |

## Aging Risk

| Content type | Risk | Review cadence |
|---|---|---|
| Specific tool version behaviors | High | Before each edition |
| Token count figures (MCP overhead) | High | Before each edition |
| Tool product status (Roo Code, Continue) | High | Before each edition |
| Compaction thresholds | High | Before each edition |
| Instruction file empirical findings | Medium | Every 2 years |
| Cross-tool portability matrix | Medium | Every year |
| Folder structure recommendations | Low | On major new evidence |
| Core context mechanics (rot, attention budget) | Low | On major new results |

**High-aging-risk mitigation:** Chapters 7, 8, 9 carry the highest aging risk. Each should include a "Last verified: [date]" note on tool-specific claims and a pointer to the official docs for current values.

---

# PART 13 — MARKET POSITIONING

## Differentiation Summary

The competitive position is clean. No existing resource occupies the CLI-agnostic diagnosis-and-repair layer:

- **Vendor docs**: cover one tool's controls; no diagnosis layer; no cross-tool synthesis
- **Marco (Packt, 2026)**: teaches Claude Code features; no failure diagnosis; no cross-tool transfer; $31.72 Kindle
- **Beginners Bible genre**: teaches prompting and use cases; no workflow architecture; no failure modes
- **Vibecoding/101-things genre**: tips for one tool; no transferable mental model
- **The v1.1 research guide**: comprehensive, cited, labeled — but organized by topic, not by problem; not actionable as a repair manual

## Primary Differentiation Statement

"The only practitioner handbook that tells you why your AI workflow is failing and how to fix it — across Claude Code, Codex, Cursor, Gemini CLI, and whatever ships next year — because it treats the filesystem as the durable operating system and every tool as a replaceable adapter."

## Market Size Estimate

- Daily CLI AI tool users: millions and growing
- Practitioner handbook Kindle buyers in this space: early market, high growth
- Price point competitive advantage: $1 vs. $31.72 (Marco) vs. $22.77 (Beginners Bible)
- KU borrows from practitioners who want a reference, not a purchase

---

# PART 14 — FEATURE LIST

| Feature | Priority | Production effort | Notes |
|---|---|---|---|
| 15-chapter architecture | ESSENTIAL | Low | |
| Copy-paste templates in every chapter | ESSENTIAL | Low | Primary value delivery |
| Source confidence labels throughout | ESSENTIAL | Low | Core differentiator |
| Three-act arc (Setup / Diagnosis / Honest) | ESSENTIAL | Low | |
| Per-chapter worked example (before/after) | ESSENTIAL | Medium | |
| Anti-patterns checklist (Ch. 12) | ESSENTIAL | Low | |
| Failure-mode catalog (Ch. 13) | ESSENTIAL | Low | |
| Per-tool instruction file table (Ch. 4) | ESSENTIAL | Low | |
| MCP scope cheat sheet (Ch. 9) | ESSENTIAL | Low | |
| Session workflow template (Ch. 6) | ESSENTIAL | Low | |
| Mini-benchmark protocol (Ch. 15) | IMPORTANT | Low | Unique in the market |
| Per-tool compaction table (Ch. 7) | IMPORTANT | Low | |
| Portability matrix (Ch. 8) | IMPORTANT | Low | |
| Governance controls template (Ch. 14) | IMPORTANT | Low | |
| Tool product status notes | IMPORTANT | Medium | Aging risk mitigation |
| Companion website / living version | ASPIRATIONAL | High | For high-aging-risk content |

**Minimum Viable Book:** ESSENTIAL features. Every ESSENTIAL feature is a copy-paste template or a reference table — low production effort. The MVB is high-value to produce.

---

# PART 15 — OUT OF SCOPE

Permanently excluded unless there is a structural revision:

| Topic | Why excluded | Better source |
|---|---|---|
| Prompt engineering theory | Different reader, different problem | Many existing resources |
| LLM architecture and training | Not relevant to workflow diagnosis | ML textbooks |
| Building MCP servers | Implementation, not usage | Vendor docs; MCP spec |
| Building CLI tools agents will call | Separate concern (Ch. 16 reference only in v1.1) | clig.dev |
| Claude Code internals (subagents, skills, output styles) | Marco covers this; outside the cross-tool thesis | Marco (2026) |
| Prompt caching optimization | Tool-specific advanced optimization | Claude Code docs |
| Multi-agent orchestration patterns (advanced) | Beyond the practitioner scope | Research papers; LangChain docs |
| Enterprise deployment and SSO | Different reader | Vendor enterprise docs |

All exclusions acknowledged in the introduction with pointers to better sources where they exist.

---

# PART 16 — ADOPTION RISK REGISTER

| # | Risk | Likelihood | Impact | Mitigation |
|---|---|---|---|---|
| 1 | Tool product status changes (Roo Code shutdown; Continue repositioning) | High | Medium | "Last verified" dates; pointer to official docs for current status |
| 2 | Compaction threshold numbers change | High | Low | Label as [CONVENTION]; point to current config files |
| 3 | AGENTS.md standard evolves | Medium | Medium | Describe behavior, not spec version; check agents.md before each edition |
| 4 | New major CLI tool enters market (post-drafting) | Medium | Medium | Chapter 8's portability matrix is extensible; tool-specific content is in sidebars |
| 5 | Empirical findings on instruction files shift | Medium | Medium | Chapter 15 presents the 2026 evidence; methodology is durable even if findings shift |
| 6 | Cursor `.md` vs `.mdc` resolution | Medium | Low | Present both; recommend testing; note the conflict explicitly |
| 7 | Claude Cowork documentation gap | Medium | Medium | Document as [UNVERIFIED] where confirmed; flag for verification before publication |
| 8 | Security threat landscape evolves (new injection patterns) | Medium | High | Chapter 14 covers principles, not specific CVEs; principles are stable |
| 9 | $1 price point sustainability | Low | High | KU strategy mitigates; update pricing before each edition as needed |

---

# PART 17 — OPEN QUESTIONS LOG

| # | Question | Stakes | Decision deadline | Owner | Status |
|---|---|---|---|---|---|
| OQ-1 | Claude Cowork global-instruction file, sub-agents, compaction commands — are any confirmed in public docs? | Ch. 8 accuracy; table completeness | Before manuscript drafting | Author | Open |
| OQ-2 | Cursor `.md` vs `.mdc` — has this been resolved in current Cursor docs? | Ch. 4 and Ch. 8 accuracy | Before manuscript drafting | Author | Open |
| OQ-3 | Which worked examples use illustrative cases vs. citable real cases? | Sourcing requirement; credibility | Before first draft | Author | Open |
| OQ-4 | Tool product status for Continue (repositioned) and Roo Code (shutdown) — confirm current state before drafting Ch. 8 | Ch. 8 accuracy | Before Ch. 8 draft | Author | Open — Roo Code shutdown May 15 2026 confirmed; Continue repositioning confirmed |
| OQ-5 | Companion website / living version for high-aging-risk content — feasible for launch or post-launch? | Ch. 7, 9 longevity | Post-launch | Author | Open |
| OQ-6 | Seth Brown as co-author / practitioner voice? | Voice and credibility; consistent with AI tool series | Before manuscript begins | Author + Seth | Open |

---

*TIKTOC.md v1.0 — All phases complete*
*Vision (i1–i4), Learning Architecture (l1–l4), Chapter Architecture (c1–c4), Scope & Market (m1–m4)*
*Ready for Cowork research pipeline*
*No blockers — OQ-1 through OQ-6 are clarifications, not blockers*
