# Agent Workflow Patterns That Actually Work

## Learning Objectives

By the end of this chapter, you should be able to:

- Name reusable agent workflow patterns.
- Select a pattern for a task.
- Write plain-language instructions that implement the pattern.
- Avoid self-grading and over-broad delegation.

## Opening Case

You ask: "Write this article, check it, and improve it." The agent writes a draft, says it checked it, and makes a few cosmetic edits. The result still has the same structural problems.

The issue is not that the agent cannot revise. The issue is that the builder and reviewer were the same context with the same blind spots.

## Core Concept

Good agent work is patterned work. Anthropic's "Building Effective AI Agents" describes workflows such as prompt chaining, routing, parallelization, orchestrator-workers, and evaluator-optimizer (https://www.anthropic.com/engineering/building-effective-agents). The practitioner version is simpler:

| Pattern | Use when |
|---|---|
| Builder-validator | Output can be checked against criteria |
| Researcher-writer-editor | Deliverable depends on evidence and voice |
| Planner-executor-reviewer | Multi-step work needs approval |
| Subagent delegation | Exploration would flood main context |
| Staging-before-output | Draft must pass validation before promotion |
| Diff-first | Change has broad blast radius |
| Test-before-write | Code behavior is uncertain |

## Worked Example

Bad:

```text
Write the chapter and make sure it is good.
```

Better:

```text
Builder: draft the chapter into staging/.
Validator: compare it against TIKTOC.md anatomy and pantry notes.
Return only missing requirements and factual risks.
Builder: revise once, then save to chapters/.
```

This works because the validator has a job, not a mood.

**The lesson:** separate roles when quality depends on judgment.

**The limit:** patterns add overhead. Do not use a three-agent workflow for a one-line edit.

## Pattern Prompts

```text
PLANNER-EXECUTOR-REVIEWER
Read relevant files only. Produce a plan. Do not edit until approved.
After editing, review the diff against the plan.

STAGING-BEFORE-OUTPUT
Write draft to staging/. Validate against PROJECT_RULES.md.
Move to outputs/ only after validation.

SUBAGENT SUMMARY
Investigate X. Return a concise summary with sources and open risks.
Do not dump raw files.
```

## When Agents Call Your CLI

Sometimes the workflow pattern is not another prompt. It is a local command. If agents, scripts, and humans will all call a CLI, design it as an agent-friendly interface:

- Put primary output on `stdout`.
- Put errors, logs, and progress on `stderr`.
- Use meaningful exit codes.
- Support `--json` for structured output.
- Support `--quiet`, `--verbose`, and `--debug`.
- Detect TTY vs. pipe; disable color when piped.
- Provide `--dry-run` for consequential actions.
- Make `--help` example-led.

This is the same principle at a lower layer: make state explicit, output parseable, and dangerous actions reversible or gated. The business logic should live behind the CLI, not inside argument parsing:

```text
core logic -> CLI adapter -> terminal/shell adapter -> packaging adapter
```

Go with Cobra, Rust with clap, Python with Click, and zero-dependency `argparse` can all work. The design rule matters more than the framework: keep the command surface thin and the behavior testable.

## Templates, Skills, and Reusable Procedures

Do not put every reusable idea into always-loaded project rules. Separate the kinds of reusable material:

| Thing | Use it for |
|---|---|
| Global instruction | Applies to every project, every time |
| Project rule | Applies to one project |
| Template | Reusable output skeleton |
| Skill/workflow | Reusable procedure with steps and checks |
| Status file | Current state and next actions |
| Manifest | Map of what to read and ignore |

A template answers "what shape should the output have?" A skill or workflow answers "what steps should the agent follow?" A project rule answers "what must always be true here?" Keeping those separate reduces fixed context cost and makes each artifact easier to test.

## Common Misconceptions

**Misconception: "More agents is more agentic."**  
More agents can mean more noise. Use patterns to reduce complexity, not display it.

**Misconception: "A critic should find all problems."**  
Unscoped critics over-report. Ask for correctness, requirements, or risk.

**Misconception: "Testing is only for software."**  
Writing can be tested against anatomy, citations, claims, and examples.

## Exercises

1. Rewrite one failed prompt as builder-validator.
2. Write a validator checklist for a chapter draft.
3. Choose a task where a simple one-shot prompt is enough.

## What Would Change My Mind

I would revise this chapter if future agents reliably self-evaluated complex outputs without role separation or independent criteria. Current evidence and practice still favor structured workflows.

## Still Puzzling

- When do subagents become coordination overhead?
- How much context should a reviewer see?
- Can tool-native review modes replace custom validator prompts?
