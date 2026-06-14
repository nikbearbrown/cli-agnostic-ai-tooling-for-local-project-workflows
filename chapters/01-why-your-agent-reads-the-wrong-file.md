# Why Your Agent Reads the Wrong File

## Learning Objectives

By the end of this chapter, you should be able to:

- Explain why an agent infers file importance from structure, names, and recent context.
- Identify three common failures: wrong canonical file, over-broad reading, and archived-vs-current confusion.
- Diagnose whether a bad answer is a model problem or a context-structure problem.
- Apply a small folder change that prevents the agent from using stale material.

## Opening Case

You ask your agent to summarize the current product plan. It answers confidently. It even sounds useful. Then you notice the problem: the answer is based on `product-plan-old.md`, not `product-plan.md`.

Nothing in the response looked broken. The model did not say, "I am using the wrong file." It did what agents often do: it inferred from nearby files, filenames, search hits, timestamps, and whatever context had already been loaded. The bad answer did not begin in the model. It began in the folder.

This is the first rule of agentic local work: the filesystem is part of the prompt.

## Core Concept

An AI agent does not enter your project with your mental model. It does not know which file is canonical unless your structure tells it. A human sees `draft-final.md`, `draft-final-real.md`, and `draft-final-june.md` and remembers the story. An agent sees three plausible candidates.

Anthropic's context-engineering guidance treats paths, filenames, folder hierarchy, and local retrieval as part of how agents build useful context (Anthropic, "Effective context engineering for AI agents," https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents). Chroma's context-rot research adds the second half of the warning: adding more context does not monotonically improve performance. Long context and distractors can degrade reliability even before a formal window limit is reached (Chroma, "Context Rot," https://www.trychroma.com/research/context-rot).

The three recurring failures are:

1. **Wrong canonical file:** the agent uses an old or secondary file as if it were source of truth.
2. **Over-broad reading:** the agent reads too many files and loses signal in noise.
3. **Archived-vs-current confusion:** old work sits beside active work, so the agent treats both as live.

The fix is not a louder prompt. The fix is a filesystem where current, archived, generated, and reference material live in physically different places.

## Worked Example

Before:

```text
project/
  chapter.md
  chapter-final.md
  chapter-final-OLD.md
  chapter-notes.md
  chapter-output.html
```

The agent is asked to revise the chapter. Which file should it read? A human may know. The agent has to infer.

After:

```text
project/
  current/
    chapter.md
  research/
    chapter-notes.md
  outputs/
    chapter-output.html
  archive/
    2026-06-old-drafts/
      chapter-final.md
      chapter-final-OLD.md
```

Now the structure teaches the rule before any instruction file loads. `current/` is active. `archive/` is old. `outputs/` is generated. `research/` supports the work but is not the work.

**The lesson:** a good folder structure is a prompt the agent cannot miss.

**The limit:** structure reduces wrong-file risk; it does not enforce security or guarantee obedience. For high-risk operations, you still need gates, tests, hooks, or human review.

## Common Misconceptions

**Misconception: "The agent will read everything and figure it out."**  
Reading everything is expensive and can make the answer worse. The context window is not a neutral bucket; irrelevant material competes with relevant material.

**Misconception: "Bigger context windows solve this."**  
Bigger windows help, but context rot is gradual. A huge window full of stale or similar files is still noisy.

**Misconception: "The filename says old, so the agent will ignore it."**  
Maybe. But "old" in a filename is weak metadata. `archive/` is stronger.

## Quick Diagnosis Template

```text
Why did the agent read the wrong file?

[ ] Old and current drafts live in the same folder.
[ ] Generated outputs sit beside source files.
[ ] There is no archive/ directory.
[ ] There is no _MANIFEST.md naming canonical files.
[ ] The task prompt was broad enough to invite a whole-folder search.

If any box is checked, fix the structure before blaming the model.
```

## Exercises

1. Find one folder you use with an AI agent. List every file that could be mistaken for canonical.
2. Move old drafts into an `archive/` directory and generated files into `outputs/` or `build/`.
3. Write one sentence that tells a future agent which file is canonical.

## What Would Change My Mind

I would revise this chapter if controlled studies showed that modern agents reliably identify canonical files in messy folders without explicit structure, even when stale and current drafts are topically similar. Current context-rot and context-engineering evidence points the other way.

## Still Puzzling

- How much do different tools rely on timestamps versus path names?
- Which folder names are most reliably interpreted across models?
- Can future IDE agents infer canonical status from human edit history better than from folder structure?

