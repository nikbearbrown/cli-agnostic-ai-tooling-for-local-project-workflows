# The Failure-Mode Catalog: Root Causes and Mitigations

## Learning Objectives

By the end of this chapter, you should be able to:

- Map a workflow symptom to a root cause.
- Identify the trigger that caused a pattern to fail.
- Choose an appropriate mitigation.
- Avoid overgeneralizing one tool's behavior.

## Opening Case

Your agent keeps reading archive files despite the manifest. You add a louder rule. It happens again. The rule was not the root cause.

The root cause was that your task prompt said "summarize everything," and the archive was physically inside the searched tree.

## Core Concept

A failure mode has three parts:

```text
pattern + trigger + mitigation
```

If you skip the trigger, you guess at fixes.

## Catalog

| Pattern | Failure | Trigger | Mitigation |
|---|---|---|---|
| Manifest tiers | Agent reads Tier 3 | Vague task or broad search | Scope prompt; physical archive; ignore where supported |
| Ignore files | Secret still visible | Confusing git ignore with security | Keep secrets outside workspace |
| Tool adapters | Rules duplicate or drift | Multiple hand-written files | Canonical source + generated adapters |
| Memory index | Critical pointer too low | Index grows too long | Keep true index; audit top section |
| `status.md` | Agent trusts stale state | Not updated at session end | End-session ritual |
| Handoff | Continuity lost | Missing decisions/reasons | Use template; include next actions |
| Long session | Quality drifts | Accumulated distractors | Handoff + fresh session |
| Reviewer | Over-reports gaps | Unscoped critique | Limit to criteria |
| Vendor figures | Bad optimization target | Unverified benchmark claims | Measure locally |
| Large data | Agent reads full dataset or repo bloats | Full files committed or left in active context | Ship sample, document fetch, ignore full data, summarize before reading |
| Generated adapters | Hand-edited generated file | No generated header or CI check | Add do-not-edit header and stale-generated-file check |

## Implementation Build Order

If you are fixing an existing project, do not start with the fancy parts. Build in this order:

1. Create the canonical folder template.
2. Add `_MANIFEST.md`, `PROJECT_RULES.md`, `status.md`, and `session-handoff.md`.
3. Make `AGENTS.md` the source of truth and add only the shims you need.
4. Add `.ai/manifest.yaml` and a tiny structure-audit script.
5. Add validator checklists and the mini-benchmark.
6. Add governance controls: permission profile, allowlists, and audit logging.

This order matters because it moves from highest leverage and most portable to most tool-specific. Do not start with a Claude hook if the project still has old drafts beside current drafts.

## Worked Example

Symptom: the agent used an old chapter outline.

Diagnosis:

```text
Pattern: status/index discipline
Trigger: outline.md and TIKTOC.md disagreed
Mitigation: declare TIKTOC.md canonical in _MANIFEST.md, update status.md, archive old outline or mark it superseded
```

Not enough:

```text
"Please use the current outline."
```

Better:

```text
_MANIFEST.md:
Tier 1 canonical: TIKTOC.md
Tier 3 archive: outline-old.md
```

**The lesson:** prompt fixes fade; structural fixes persist.

**The limit:** not every failure has one cause. Some failures combine stale state, vague prompts, and tool-specific loading.

## Common Misconceptions

**Misconception: "The symptom tells me the fix."**  
The same symptom can have multiple causes.

**Misconception: ".gitignore is a privacy boundary."**  
It is a version-control boundary, not necessarily an agent-read boundary.

**Misconception: "If one tool failed, all tools will fail the same way."**  
Tool loading and ignore behavior differ.

## Exercises

1. Write a failure report for one agent mistake: symptom, trigger, mitigation.
2. Pick one stale state file and update it.
3. Find one rule that is advisory and propose an enforcement layer.

## What Would Change My Mind

I would revise this catalog if behavior-driven agent testing identified a better taxonomy. Emerging work such as ABTest-style agent behavior testing suggests this area will become more empirical over time [verify].

## Still Puzzling

- Can tools automatically detect stale manifests?
- Which failures are easiest to prevent structurally?
- How should teams collect failure reports without creating bureaucracy?
