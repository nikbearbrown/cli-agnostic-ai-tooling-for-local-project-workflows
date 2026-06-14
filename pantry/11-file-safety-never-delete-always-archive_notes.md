# Research Notes: Chapter 11 - File Safety: Never Delete, Always Archive

**Source:** TIKTOC.md chapter entry
**Notes file:** 11-file-safety-never-delete-always-archive_notes.md
**Corresponding chapter:** chapters/11-file-safety-never-delete-always-archive.md (not yet written)
**Generated:** 2026-06-14

---

## Chapter summary from TIKTOC.md

The archive-not-delete rule and destructive-action gates prevent filesystem disasters. The chapter contrasts instruction files, hooks, git, and in-tool checkpoints.

---

## A. Conceptual foundations

### Archive is safer than delete

For agent workflows, delete should not be the default. Moving to `archive/` preserves recovery while still cleaning the active surface.

**Common misconception:** "Git makes deletion safe." Git helps only if the file was tracked and committed.

**Worked example:** Agent wants to remove superseded drafts. It moves them to `archive/2026-06-14/` and reports the list.

**Source(s):** Git docs for recovery/version control context; practitioner convention.

### Gates should protect irreversible/high-blast-radius actions

Not every operation should require confirmation. Reads and small reversible edits should flow. Deletes, bulk renames, canonical overwrites, network writes, and force pushes require gates.

**Common misconception:** "More approvals means safer." Too many approvals train users to click through and slow harmless work.

**Worked example:** Gate `rm`, `mv chapters/*`, `git push --force`, and writes to production config.

**Source(s):** Claude hooks docs; general least-privilege practice.

### Hooks and permissions are enforcement layers

Instruction files are advisory. Hooks, permission policies, wrappers, tests, and git pre-commit checks can make some rules deterministic.

**Common misconception:** "A no-delete sentence is enough." It should be backed by a guard when loss is unacceptable.

**Worked example:** Claude PreToolUse hook denies `rm` unless target is known rebuildable cache.

**Source(s):** Claude Code hooks docs, https://code.claude.com/docs/en/hooks

---

## B. Domain examples and cases

### Case 1: Book cleanup

Instead of deleting placeholder drafts, archive them. The writer can recover if the agent misunderstood "obsolete."

### Case 2: Code generated artifacts

Deleting `build/` output is safe if it can be regenerated. Deleting `src/` or `chapters/` is not.

### Failure case: vague cleanup

"Clean this repo" without constraints leads to high-blast-radius guessing. The fix is target, constraint, and done criteria.

---

## C. Connections and dependencies

**Prerequisites:**
- Chapter 2 folder roles.
- Chapter 4 advisory vs enforcement.

**Unlocks:**
- Chapter 12 anti-pattern audit.
- Chapter 14 governance controls.

**Adjacent chapter connections:**
- Chapter 10 approval gates.
- Chapter 12 common anti-patterns.

---

## D. Current state of the field

**Settled:**
- Git is essential but not sufficient for file safety.
- Hook/permission systems can enforce behavior better than prose rules.

**Contested or emerging:**
- Tool-specific checkpoint systems vary and should not be treated as portable recovery.
- Best cross-tool guardrails often require external scripts or wrappers.

**Key references:**
1. Git `gitignore` and git workflow docs.
2. Claude hooks docs.
3. Claude memory docs on instructions vs enforced settings.

**Recent developments:**
- Agent tools increasingly expose checkpoints/rewind, but durable recovery still belongs in git and archive conventions.

---

## E. Teaching considerations

**Where students get stuck:**
- They trust untracked files to be recoverable.
- They over-gate and make the workflow unusable.

**Analogies and framings that work:**
- Archive is a quarantine shelf, not a trash can.

**Exercises:**
- Identify three irreplaceable files and their current protection.
- Ask an agent to propose a cleanup plan without executing; evaluate blast radius.

---

## Local library cross-references

- `_lib_ai-software-engineering-at-google-lessons-learned-from-programming-over-time.md`

