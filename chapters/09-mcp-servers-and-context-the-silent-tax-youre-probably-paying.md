# MCP Servers and Context: The Silent Tax You're Probably Paying

## Learning Objectives

By the end of this chapter, you should be able to:

- Explain why MCP servers can add fixed and per-call context cost.
- Audit a tool configuration for over-provisioned MCP servers.
- Scope MCP use by project or task.
- Reduce payload cost through filtering and aggregation.

## Opening Case

You added a GitHub MCP server. Then Slack. Then Drive. Then a database. Then a web search server. Every addition made sense. But now even simple sessions feel slow and noisy.

You did not add one tool. You added a tool surface.

## Core Concept

The Model Context Protocol connects AI hosts to external tools and data sources (MCP specification, https://modelcontextprotocol.io/specification/2025-11-25/basic/lifecycle). That is powerful. It also means the agent may see more tool descriptions, more possible actions, and more returned data.

Anthropic's "Code execution with MCP" explains the context problem: tool schemas and intermediate payloads can consume substantial context, and moving intermediate processing into code execution can reduce what the model must see (https://www.anthropic.com/engineering/code-execution-with-mcp).

The practical rule:

```text
Load the smallest MCP surface that can do the task.
Return the smallest payload that preserves evidence.
```

## Worked Example

Bad tool output:

```json
[
  {"id": "...", "created_at": "...", "updated_at": "...", "metadata": {...}, "amount": 42},
  ...
]
```

Better tool output:

```json
{
  "query": "spend_by_month",
  "date_range": "2026-01 through 2026-06",
  "records_count": 1842,
  "monthly_totals": [
    {"month": "2026-01", "total": 1204.55}
  ],
  "source": "transactions table"
}
```

The second output is smaller and more useful. It preserves provenance without dumping the database.

**The lesson:** MCP should move work out of context, not flood context.

**The limit:** exact token costs vary by tool, schema, and client. Treat dramatic percentage claims as examples until measured locally.

## MCP Audit

```text
[ ] List active MCP servers.
[ ] Mark each as always-needed, project-needed, or one-off.
[ ] Disable one-off servers by default.
[ ] Prefer project-specific config over global config.
[ ] Filter fields before returning data.
[ ] Aggregate in the tool when possible.
[ ] Log which connector supplied which claim.
```

## Common Misconceptions

**Misconception: "More MCP servers means better agent."**  
More servers can mean more ambiguity, cost, and risk.

**Misconception: "Only tool results cost context."**  
Tool schemas and descriptions can also be part of the model's tool context.

**Misconception: "Raw data is more honest."**  
Raw data is sometimes necessary. Often, a computed aggregate plus provenance is more useful.

## Exercises

1. Inventory every MCP server you have enabled.
2. Disable all but one and run a common task.
3. Rewrite a raw payload into a compact evidence-preserving response.

## What Would Change My Mind

I would revise this chapter if MCP clients broadly adopted dynamic tool retrieval and stopped exposing large unused schemas by default. Current practice still requires active pruning.

## Still Puzzling

- Which clients expose tool schema cost clearly?
- Can MCP servers declare lightweight and heavyweight modes?
- What is the right default for personal productivity connectors?

