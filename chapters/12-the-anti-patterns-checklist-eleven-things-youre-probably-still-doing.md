# The Anti-Patterns Checklist: Eleven Things You're Probably Still Doing

## Learning Objectives

By the end of this chapter, you should be able to:

- Audit a project against eleven common agent workflow anti-patterns.
- Prioritize fixes by impact.
- Match each anti-pattern to its structural repair.

## Opening Case

You have fixed one problem at a time. You added a manifest. You shortened a rules file. You moved old drafts. But something still feels off.

This chapter is the wall checklist.

## Core Concept

Most agent workflow failures are not mysterious. They are repeated boundary failures: project boundaries, source/output boundaries, current/archive boundaries, session boundaries, and tool boundaries.

Use this checklist as a 15-minute audit.

## The Checklist

```text
[ ] 1. Pointing the agent at a giant parent folder
    Fix: one bounded project root.

[ ] 2. Mixing unrelated projects in one session
    Fix: separate sessions and handoffs.

[ ] 3. Keeping old drafts beside current drafts
    Fix: archive/ for superseded work.

[ ] 4. Letting outputs become source
    Fix: mark build/ and outputs/ as non-canonical.

[ ] 5. Huge global memory or instruction files
    Fix: short rules; move detail to task-specific docs.

[ ] 6. Many unrelated tasks in one session
    Fix: one task per thread.

[ ] 7. Dumping full logs or JSON into context
    Fix: summarize, filter, aggregate.

[ ] 8. Asking "what is in this folder?" every session
    Fix: maintain status.md.

[ ] 9. Vague tasks such as "clean this up"
    Fix: target, constraint, done criteria.

[ ] 10. Letting the agent delete or rename without review
    Fix: archive-not-delete and destructive gates.

[ ] 11. Depending on tool-specific behavior
    Fix: encode intent in portable files plus adapters.
```

## Worked Example

A book repo has no manifest, old drafts in `chapters/`, generated EPUB in the same folder, and a long chat session that has handled research, drafting, image prompts, and build debugging.

Audit results:

```text
3: old drafts beside current drafts
4: outputs becoming source
6: unrelated tasks in one session
8: no status.md
```

Fix order:

1. Move output to `output/`.
2. Move old drafts to `archive/`.
3. Write `status.md`.
4. Start a fresh session from handoff.

**The lesson:** fix the boundary causing the current failure first.

**The limit:** checklists diagnose; they do not replace judgment.

## Common Misconceptions

**Misconception: "I need to fix all eleven now."**  
No. Fix the highest-risk three.

**Misconception: "Anti-patterns mean I did something wrong."**  
They mean the project evolved faster than its structure.

**Misconception: "A checklist is beginner material."**  
Experts use checklists because repeated work fails in repeated ways.

## Exercises

1. Run the checklist on your most active project.
2. Choose the top three fixes by risk reduction per hour.
3. Re-run the checklist one week later.

## What Would Change My Mind

I would revise this checklist if empirical studies showed different failure clusters in real agent sessions. For now, it synthesizes the strongest recurring failures in current practice and research.

## Still Puzzling

- Which anti-pattern predicts the most downstream failures?
- Should teams score anti-patterns in CI?
- How often should the checklist be rerun?

