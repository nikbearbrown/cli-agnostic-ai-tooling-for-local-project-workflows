# The Greenfield Project: What Clean Looks Like

## Learning Objectives

By the end of this chapter, you should be able to:

- Build a folder structure that separates canonical, transient, generated, and archived material.
- Explain why folder names are metadata for agents.
- Identify which folders an agent should read by default and which it should ignore.
- Retrofit a messy project into a clean agent-readable structure.

## Opening Case

Most agent projects begin innocently. You ask for one draft. Then another. Then a figure. Then a build artifact. Then a "quick" research note. Three weeks later your project has `final.md`, `final2.md`, `notes.md`, `notes-old.md`, `output.html`, and `research-dump.md` in the same folder.

Nothing feels broken until the agent starts using the wrong thing as source.

Clean is not aesthetic. Clean is operational. A clean project tells the agent what kind of thing each file is before the file is opened.

## Core Concept

Use this structure as the default for any project you expect an AI CLI, desktop agent, or future automation to touch:

```text
project/
  _PROJECT_INDEX.md
  AGENTS.md
  _MANIFEST.md
  PROJECT_RULES.md
  status.md
  session-handoff.md
  .ai/
    manifest.yaml
    workflows/
    schemas/
    sessions/
    audit/
  src/
  current/
  research/
  templates/
  staging/
  build/
  outputs/
  archive/
```

The names matter because agents use path structure as context. Anthropic's context-engineering work explicitly treats file organization as a way to help agents retrieve relevant material without flooding context (https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents).

The roles are simple:

| Folder | Role |
|---|---|
| `src/` | Canonical source for software or structured artifacts |
| `current/` | Active drafts being edited now |
| `research/` | Evidence and notes |
| `templates/` | Reusable skeletons |
| `staging/` | Drafts awaiting validation |
| `build/` | Regenerable intermediates |
| `outputs/` | Finished deliverables |
| `archive/` | Superseded material, ignored unless requested |
| `.ai/` | Machine-readable workflow metadata |

## Worked Example

Before:

```text
client-report/
  report.md
  report-old.md
  report-final.pdf
  sources.md
  prompt.txt
  chart.svg
  scratch.json
```

After:

```text
client-report/
  current/
    report.md
  research/
    sources.md
  templates/
    prompt.txt
  outputs/
    report-final.pdf
  images/
    chart.svg
  build/
    scratch.json
  archive/
    report-old.md
```

The agent no longer has to guess that the PDF is output, not source. The role is in the path.

**The lesson:** put meaning in folder boundaries, not just filenames.

**The limit:** exact folder names are convention, not law. If your repo already uses `output/` instead of `outputs/`, keep it, but document the role in `_MANIFEST.md`.

## Workspace Index and Git Hygiene

If you manage many projects, add one workspace-level index:

```markdown
# _PROJECT_INDEX.md

| Project | Status | Updated | One-line state | Path |
|---|---|---|---|---|
| cli-tooling-book | active | 2026-06-14 | drafting chapters | projects/cli-tooling-book/ |
| data-pipeline | paused | 2026-06-01 | awaiting review | projects/data-pipeline/ |
```

This lets an agent identify the live project without opening every project folder. In a multi-book, multi-client, or multi-repo workspace, that small table can prevent a lot of waste.

Also decide what belongs in version control. Generated layers should usually be ignored:

```gitignore
build/
outputs/
output/
.ai/audit/
.ai/sessions/
__pycache__/
*.pyc
node_modules/
```

That is not a security boundary. `.gitignore` keeps generated files out of git; it does not necessarily keep an agent from reading local files. Use it to keep history clean, not to hide secrets.

## Common Misconceptions

**Misconception: "This is too much structure for a small project."**  
Most of these folders can start empty. The point is to create rails before files accumulate.

**Misconception: "Generated output is the final truth."**  
Generated output is often what humans read, but it is not what the agent should edit. The source is whatever regenerates it.

**Misconception: "I can mix projects if the agent is smart."**  
Pointing an agent at a giant parent folder invites cross-project confusion.

## Copy-Paste Setup

```bash
mkdir -p .ai/{workflows,schemas,sessions,audit}
mkdir -p src current research templates staging build outputs archive
touch _PROJECT_INDEX.md AGENTS.md _MANIFEST.md PROJECT_RULES.md status.md session-handoff.md .ai/manifest.yaml
```

## Exercises

1. Create this structure in a scratch project.
2. Take ten files from an existing project and assign each to one destination folder.
3. Write a one-line rule for `outputs/`: "Files here are..."

## What Would Change My Mind

I would revise this chapter if agent tools adopted a reliable, cross-vendor project metadata standard that made folder role names unnecessary. Today, plain folder structure remains the most portable metadata layer.

## Still Puzzling

- Should `.ai/` become a real community convention?
- Is `current/` useful in software repos, or mainly writing/research repos?
- How should teams name generated output when existing build systems already use `dist/`, `target/`, or `out/`?
