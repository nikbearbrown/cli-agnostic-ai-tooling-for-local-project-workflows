# File Safety: Never Delete, Always Archive

## Learning Objectives

By the end of this chapter, you should be able to:

- Write archive-not-delete rules for agent work.
- Identify destructive operations that need approval.
- Distinguish instruction, hook, checkpoint, and git safety layers.
- Design a file-safety policy for one project.

## Opening Case

You ask the agent to "clean up the project." It deletes files. Some were generated. Some were old. Some were the only copy of work you had not committed.

The dangerous word was not "delete." It was "clean."

## Core Concept

Agents are good at executing ambiguous verbs. That is exactly the problem. "Clean," "simplify," "tidy," and "remove clutter" can turn into high-blast-radius file operations.

The default rule should be:

```text
Never permanently delete files. Move them to archive/ instead.
Ask before bulk renames, overwrites of canonical files, or structural moves.
```

Git helps, but only for files that are tracked and committed. Tool-native checkpoints help, but they are not portable. Claude hooks can enforce specific command guards in Claude Code (https://code.claude.com/docs/en/hooks), but other tools need other mechanisms.

For a rule you actually care about, advisory text is only the floor. Back it with a deterministic guard where the tool allows it: a shell wrapper, permission profile, pre-commit hook, or Claude Code `PreToolUse` hook. A no-delete hook can allow rebuildable targets such as `.build/`, `__pycache__/`, `*.pyc`, and `*.bak`, while denying `rm` against source, data, logs, or chapters.

## Worked Example

Unsafe prompt:

```text
Clean up this folder.
```

Safer prompt:

```text
Identify files that appear superseded. Do not delete or move anything.
Return a proposed archive plan with source path, destination path, and reason.
Wait for approval.
```

After approval:

```text
Move superseded files to archive/2026-06-14-cleanup/.
Report every move.
```

**The lesson:** destructive work needs a plan before action.

**The limit:** archive folders can become dumps. Periodically summarize or date them.

## Safety Layers

| Layer | What it does | Limit |
|---|---|---|
| Instruction file | Tells agent preferred behavior | Advisory |
| Hook/permission | Blocks specific actions | Tool-specific |
| Git commit | Durable recovery | Only committed/tracked files |
| Archive folder | Recoverable cleanup | Can grow noisy |
| Human approval | Judgment gate | Slows flow if overused |

## Large Files and Data Safety

Large files create a different safety problem from deletion. Do not confuse these cases:

| Problem | Correct response |
|---|---|
| Too big for repo history | Ship a sample; ignore or fetch full file on demand |
| Should not be published | `.gitignore`, but agent may still read it locally |
| Should not be read | Keep it outside the workspace entirely |

Many AI workflows need a simple data pattern: commit a small sample, document the fetch command, and keep full generated datasets out of history. `.gitignore` stops future tracking; it does not shrink past history and it does not hide data from an agent with local filesystem access.

## Common Misconceptions

**Misconception: "Git means deletion is safe."**  
Not if the file is untracked or uncommitted.

**Misconception: "The agent knows what clutter is."**  
Clutter is a human judgment.

**Misconception: "All file operations need approval."**  
Gate irreversible or high-blast-radius operations, not every edit.

## Exercises

1. Write a no-delete rule into your project instructions.
2. Identify three operations that require approval in your repo.
3. Ask an agent for a cleanup plan without allowing execution.

## What Would Change My Mind

I would revise this chapter if all major tools provided reliable, cross-platform, inspectable rollback for every file operation, including untracked files. Today, archive and git are still the durable portable layers.

## Still Puzzling

- Should archive folders be inside or outside the repo?
- How should agents handle large generated files that are safe to delete?
- Can a generic destructive-action classifier work across shells?
