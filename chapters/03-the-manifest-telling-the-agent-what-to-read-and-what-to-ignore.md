# The Manifest: Telling the Agent What to Read and What to Ignore

## Learning Objectives

By the end of this chapter, you should be able to:

- Explain what a manifest does and what it does not do.
- Write a `_MANIFEST.md` with Tier 1, Tier 2, and Tier 3 sections.
- Create a machine-readable `.ai/manifest.yaml`.
- Identify the main failure mode of manifest files: staleness.

## Opening Case

You ask the agent to find the latest source for a claim. It searches the whole project. It reads a 200-file archive. It summarizes the wrong note. Forty minutes later the session is heavier, slower, and less reliable.

The problem was not lack of intelligence. The problem was lack of a map.

## Core Concept

A manifest is a small index. It tells the agent what is canonical, what is task-relevant, and what should be ignored unless requested.

It is not a place to store content. It is not a second README. It is not a long explanation of the project. A good manifest is short enough to read every session.

The pattern appears across tools in different forms. Anthropic Skills use small metadata first, detailed resources later. Claude Code memory uses compact entry points and on-demand detail (https://code.claude.com/docs/en/memory). Aider's repo map gives the model a token-budgeted map of files and symbols before it reads source files (https://aider.chat/docs/repomap.html). `AGENTS.md` is emerging as a portable instruction standard for agents (https://agents.md/).

Your project manifest should be simpler than all of that:

```markdown
# _MANIFEST.md - read this first

## Tier 1 - Canonical
| File | Purpose |
|---|---|
| PROJECT_RULES.md | Project-specific rules |
| status.md | Current state |
| outline.md | Structure/source of truth |

## Tier 2 - Task Relevant
| Folder | Use when |
|---|---|
| current/ | Editing active material |
| research/current/ | Checking evidence |
| templates/ | Creating repeatable outputs |

## Tier 3 - Ignore Unless Requested
| Folder | Rule |
|---|---|
| archive/ | Ignore unless explicitly requested |
| build/ | Generated, not source |
| outputs/ | Deliverables, not working source |
```

## Worked Example

The task: "Update Chapter 4 with current sources."

Without a manifest, the agent scans:

```text
chapters/
pantry/
archive/
outputs/
notes-old/
```

With a manifest, it reads:

```text
TIKTOC.md
status.md
pantry/04-project-rules-and-instruction-precedence_notes.md
chapters/04-project-rules-and-instruction-precedence.md
```

That is enough. The archive stays quiet.

**The lesson:** a manifest makes just-in-time context possible.

**The limit:** a stale manifest misleads the agent. Update it when canonical files, folder roles, or project status changes.

## Machine-Readable Twin

```yaml
name: project-alpha
canonical:
  - PROJECT_RULES.md
  - status.md
  - outline.md
task_relevant:
  - current/
  - research/current/
  - templates/
ignore:
  - archive/
  - build/
  - outputs/
entrypoints:
  test: "npm test"
  build: "npm run build"
invariants:
  - "Never treat outputs/ or build/ as source."
  - "Move superseded files to archive/, never delete."
```

## Common Misconceptions

**Misconception: "The manifest enforces behavior."**  
No. It informs behavior. Enforcement requires permissions, hooks, tests, wrappers, or human review.

**Misconception: "The manifest should list every file."**  
No. It should list roles and canonical entry points.

**Misconception: "Once written, it is done."**  
No. A manifest is a living index.

## Exercises

1. Write a `_MANIFEST.md` for a real project.
2. Move one folder into Tier 3 and explain why.
3. Write `.ai/manifest.yaml` for the same project.

## What Would Change My Mind

I would revise this chapter if tools converged on an enforceable cross-vendor manifest standard with reliable ignore semantics. Until then, Markdown plus YAML is the most portable compromise.

## Still Puzzling

- Should `_MANIFEST.md` and `.ai/manifest.yaml` be generated from one source?
- How often should a manifest be audited?
- Can tools warn when a manifest points to missing files?

