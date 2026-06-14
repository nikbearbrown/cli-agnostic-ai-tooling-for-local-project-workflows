# Does Any of This Actually Help? Measuring Your Workflow

## Learning Objectives

By the end of this chapter, you should be able to:

- Treat instruction files as measurable artifacts.
- Run a small with-rules/without-rules benchmark.
- Record acceptance rate, manual edits, time, cost, and risky behavior.
- Prune rules that do not earn their context cost.

## Opening Case

You added `AGENTS.md`, `_MANIFEST.md`, project rules, hooks, and handoffs. The project feels more organized. But does it actually work better?

That question is not rude. It is the point.

## Core Concept

Instruction files are not sacred. They cost context. They can help, hurt, or do nothing depending on task, tool, repo, and rule quality.

The honest practice is to measure. Recent empirical work has begun testing agent manifests, AGENTS-style files, and behavior-driven agent evaluation [verify exact results before publication: arXiv 2601.20404, arXiv 2509.14744, arXiv 2604.03362]. The details will change, but the lesson is stable: do not assume a rule helps because it sounds wise.

## Mini-Benchmark

Run the same task suite with and without the rules file.

```text
1. Repo summary
2. Narrow bug fix
3. Multi-file feature
4. Test repair
5. Security-sensitive change
```

Record:

```text
- Acceptance rate
- Manual edits after agent output
- Time to valid diff
- Token or cost estimate
- Risky behavior
- Out-of-scope files touched
```

Also measure maintenance cost:

```text
- Rules file word count
- Number of adapters generated or hand-maintained
- Number of stale rules found
- Number of tool-specific claims needing re-verification
- Number of private/large/generated files accidentally loaded
```

## Worked Example

Rules file before:

```text
4,800 words
duplicates README
contains old build command
contains useful no-delete rule
contains useful test command
```

Benchmark result:

```text
No-delete rule prevented one risky action.
Old build command caused two failed runs.
Style guidance made no measurable difference.
```

After:

```text
900 words
keeps no-delete, test command, manifest rule
removes stale build command and duplicated README
```

**The lesson:** keep rules that change behavior; remove rules that only make you feel safer.

**The limit:** small benchmarks are noisy. Use them to prune obvious waste, not to declare universal truth.

## Common Misconceptions

**Misconception: "If a rule is good, more detail is better."**  
Detail costs context. Move detail into task-specific docs when possible.

**Misconception: "One successful run proves the setup."**  
You need repeated tasks or at least comparable before/after trials.

**Misconception: "Measurement is only for teams."**  
One person can still track time, edits, and risky behavior.

**Misconception: "If it is in the guide, it belongs in my project."**  
No. The implementation order is deliberately staged. A solo writing project may need folder structure, manifest, status, and no-delete rules. It may not need generated adapters, MCP governance, or a structure-audit script yet.

## Exercises

1. Run one task with your rules file and once without it in a disposable copy.
2. Remove one rule that did not affect behavior.
3. Add one enforcement mechanism for a rule that matters.

## What Would Change My Mind

I would revise this chapter if strong replicated studies showed that well-structured instruction files consistently improve outcomes across tools without meaningful context cost. Until then, the safest claim is local measurement.

## Still Puzzling

- Which task types benefit most from rules?
- What metrics best capture review burden?
- Can tools automatically report whether rules were used?
