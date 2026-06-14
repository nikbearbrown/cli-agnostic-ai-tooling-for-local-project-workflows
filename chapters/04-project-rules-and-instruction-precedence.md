# Project Rules and Instruction Precedence

## Learning Objectives

By the end of this chapter, you should be able to:

- Explain why instruction precedence differs across tools.
- Write a `PROJECT_RULES.md` with an explicit precedence statement.
- Distinguish advisory rules from enforced rules.
- Bridge one canonical rule file into multiple tools.

## Opening Case

You put "never delete files" in `CLAUDE.md`. Claude Code mostly obeys. Then you open the same project in another tool and the rule disappears. The project did not change. The tool's instruction-loading model did.

That is the problem with assuming one vendor's instruction file is your workflow architecture.

## Core Concept

Instruction files are not universal. Claude Code reads `CLAUDE.md`. Codex uses `AGENTS.md` (OpenAI Codex docs, https://developers.openai.com/codex/guides/agents-md). Aider can read convention files when configured (https://aider.chat/docs/usage/conventions.html). Cursor, Gemini, Copilot, and Cline each have their own rule locations and precedence models. `AGENTS.md` is the strongest current cross-agent candidate (https://agents.md/), but not every tool treats it the same way.

The portable strategy is:

1. Keep one canonical rules source.
2. Add thin tool-specific adapters.
3. State precedence explicitly in the project.
4. Enforce high-risk rules outside prose.

Use confidence labels when a rule depends on current vendor behavior:

```text
[OFFICIAL]    vendor docs or published spec
[CONVENTION]  common practitioner pattern
[INFERRED]    reasoned recommendation
[TOOL]        tool-specific behavior
[AGNOSTIC]    designed to hold across tools
```

These labels prevent a dangerous slide: treating a Claude Code command, a Cursor convention, or a practitioner-reported threshold as if it were a cross-tool law.

Use this sentence:

```markdown
If these project rules conflict with broader defaults, follow this file unless the user explicitly says otherwise.
```

That sentence will not force compliance, but it gives every agent the same local hierarchy.

## Worked Example

Canonical file:

```text
AGENTS.md
```

Claude adapter:

```markdown
@AGENTS.md
```

Aider adapter:

```yaml
read: AGENTS.md
```

Gemini adapter:

```markdown
# GEMINI.md
Read AGENTS.md first. Treat it as the project instruction source.
```

Now the project has one source of truth and three bridges.

For larger projects, bridges can still drift. The stronger pattern is to compile adapters. Keep shared rule modules in one source folder:

```text
instructions/
  manifest.yml
  _shared/
    no-delete.md
    completion-report.md
    conformance-gate.md
  project.md
```

Then generate:

```text
AGENTS.md
CLAUDE.md
GEMINI.md
.github/copilot-instructions.md
.cursor/rules/project.mdc
```

Each generated file should begin with a warning:

```html
<!-- GENERATED FILE - do not edit by hand.
     Source: instructions/manifest.yml
     Rebuild: scripts/build-instructions.mjs -->
```

This makes shared rules genuinely shared while still allowing tool-specific sections. The cost is a small build step and the discipline to treat generated adapter files as outputs.

**The lesson:** duplicate less; adapt more.

**The limit:** instruction files are context. A dangerous command still needs a hook, permission profile, test, or approval gate.

## `PROJECT_RULES.md` Template

```markdown
# PROJECT_RULES.md

If these rules conflict with broader/global defaults, follow THIS file
unless I explicitly say otherwise in chat.

## Source of truth
- Read `_MANIFEST.md` first.
- Treat Tier 1 files as canonical.
- Do not use `archive/` unless explicitly requested.

## File safety
- Never permanently delete files. Move superseded files to `archive/`.
- Ask before renaming or overwriting canonical files.
- Show a diff before broad changes.

## Output rules
- Save drafts to `staging/`.
- Save final deliverables to `outputs/`.
- Do not treat `outputs/` or `build/` as source.

## Task behavior
- Load only the files needed for the current task.
- State assumptions before broad changes.
- Stop if two Tier 1 files conflict.
```

## Common Misconceptions

**Misconception: "Loaded means enforced."**  
Loaded means the model can see it. Enforced means a system blocks violations.

**Misconception: "I need a full rules file for every tool."**  
You need one canonical file and adapters.

**Misconception: "Precedence is obvious."**  
It is not. Write it down.

## Exercises

1. Inventory every instruction file in one project.
2. Mark each as canonical, adapter, local preference, or generated.
3. Convert one duplicated tool file into a thin adapter.

## What Would Change My Mind

I would revise this chapter if all major tools adopted the same instruction-file name, scope, and precedence model. Current tools do not.

## Still Puzzling

- Will `AGENTS.md` become universal or remain one standard among several?
- Should project rules be generated from structured YAML?
- How much rule text is too much before it becomes fixed context waste?
