# One Folder, Many Tools: Making Cross-Tool Workflows Work

## Learning Objectives

By the end of this chapter, you should be able to:

- Explain why one folder can serve many agent tools.
- Use `AGENTS.md` as a canonical instruction source.
- Add thin adapters for tools that need different filenames.
- Classify workflow patterns as portable, adaptable, or tool-specific.

## Opening Case

Your Claude setup works. Then you try Codex. Then Cursor. Then Aider. Each tool sees a slightly different project because each reads a different instruction file. The folder is the same, but the rules are not.

That is how cross-tool workflows rot.

## Core Concept

Tool-agnostic does not mean tool-free. It means the durable intent lives in files any tool can read, while tool-specific files are adapters.

Use this rule:

```text
AGENTS.md = canonical shared instructions
CLAUDE.md / GEMINI.md / .cursor/rules / .aider.conf.yml = adapters
```

`AGENTS.md` is the best current portable candidate (https://agents.md/). OpenAI Codex documents AGENTS.md as its project instruction format (https://developers.openai.com/codex/guides/agents-md). Claude can import shared files from CLAUDE.md (Claude Code memory docs, https://code.claude.com/docs/en/memory). Aider can be configured to read convention files (https://aider.chat/docs/usage/conventions.html).

## Worked Example

The shared file:

```markdown
# AGENTS.md

Read _MANIFEST.md first.
Never delete; archive instead.
Do not treat outputs/ as source.
Run tests before reporting done.
```

Claude adapter:

```markdown
@AGENTS.md

## Claude Code
Use plan mode before broad edits.
```

Aider adapter:

```yaml
read: AGENTS.md
```

Gemini adapter:

```markdown
# GEMINI.md
Read AGENTS.md as the project instruction source.
```

**The lesson:** one source, many adapters.

**The limit:** adapters can still drift if hand-maintained. Mature projects should generate them.

## Portability Matrix

| Pattern | Classification |
|---|---|
| Folder architecture | Fully portable |
| `_MANIFEST.md` | Portable with adaptation |
| `status.md` and handoff | Fully portable |
| `PROJECT_RULES.md` | Portable if referenced by loaded instructions |
| Hooks | Tool-specific |
| Compaction commands | Tool-specific |
| MCP config | Concept portable, config tool-specific |

## Ignore Files Are Adapters Too

The manifest says "ignore Tier 3." Ignore files are one way to make a particular tool behave closer to that rule. There is no single cross-tool `.llmignore` standard. Current tools use different files:

| Tool | Ignore file |
|---|---|
| Aider | `.aiderignore` |
| Cursor | `.cursorignore` / `.cursorindexingignore` |
| Continue | `.continueignore` |
| Cline | `.clineignore` |
| Claude Code | `.gitignore` plus permissions/settings; no universal `.llmignore` |

The important distinction: `.gitignore` controls version control. Tool ignore files control indexing or context, and often only best-effort. Neither should be treated as a secret vault. If a file is genuinely sensitive, keep it out of the folder.

## Reference, Bridge, Compile

You have three levels of cross-tool robustness:

1. **Reference:** one file tells the agent to read another.
2. **Bridge:** one tool file imports or points to the canonical file.
3. **Compile:** generated adapters are built from shared instruction modules.

Use reference for quick solo work, bridge for ordinary projects, and compile once multiple adapters are likely to drift.

## Common Misconceptions

**Misconception: "Tool-agnostic means lowest common denominator."**  
No. Use tool-specific power, but keep the source of truth portable.

**Misconception: "Symlink everything."**  
Symlinks can be fragile across Windows and tool environments. Imports or generated files are often safer.

**Misconception: "Each tool deserves custom rules."**  
Only tool behavior deserves custom rules. Project truth should not duplicate.

## Exercises

1. List every AI-tool instruction file in one repo.
2. Pick the canonical file.
3. Convert every other file into an adapter.

## What Would Change My Mind

I would revise this chapter if a single cross-vendor instruction mechanism became mandatory and consistently implemented. Today, adapters remain necessary.

## Still Puzzling

- How many tools will adopt AGENTS.md natively?
- Should adapters be generated automatically?
- How should teams test instruction drift?
