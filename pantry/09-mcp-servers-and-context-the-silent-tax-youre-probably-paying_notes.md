# Research Notes: Chapter 09 - MCP Servers and Context: The Silent Tax You're Probably Paying

**Source:** TIKTOC.md chapter entry
**Notes file:** 09-mcp-servers-and-context-the-silent-tax-youre-probably-paying_notes.md
**Corresponding chapter:** chapters/09-mcp-servers-and-context-the-silent-tax-youre-probably-paying.md (not yet written)
**Generated:** 2026-06-14

---

## Chapter summary from TIKTOC.md

MCP servers expose tool schemas and connector payloads that can become fixed or per-call context cost. This chapter teaches MCP audit, scoping, and reduction strategies.

---

## A. Conceptual foundations

### MCP as integration standard

The Model Context Protocol standardizes connections between AI hosts and external tools/data sources. It solves the integration problem but expands the set of tool descriptions and external data the model may need to reason over.

**Common misconception:** "MCP is just free capability." Every connected server expands the tool surface and potential context/safety burden.

**Worked example:** A coding session does not need Slack, Google Drive, database, browser, and calendar tools all at once. Load the few needed for the task.

**Source(s):** MCP specification, https://modelcontextprotocol.io/specification/2025-11-25/basic/lifecycle; Anthropic code execution with MCP.

### Tool schema and payload cost

Tool definitions describe what tools exist and how to call them. Payloads are the data returned by tool calls. Both can be expensive, especially if raw JSON or large logs are passed through the model.

**Common misconception:** "The cost is only the data returned." The tool contract itself may also be context the model sees.

**Worked example:** Instead of returning all transactions, a finance MCP tool returns `monthly_total`, `count`, `date_range`, and `source_query`.

**Source(s):** Anthropic, "Code execution with MCP."

### Code execution and workflow engines as mitigations

Anthropic argues that code execution with MCP can keep intermediate payloads out of the model context by letting the agent write/run code in a sandbox. Emerging research proposes proactive tool retrieval and workflow engines to avoid injecting large tool sets.

**Common misconception:** "The only fix is fewer tools." Fewer tools is the first fix; better tool architecture is the deeper fix.

**Worked example:** A script calls MCP tools, filters records, computes summary, and returns 20 lines instead of 20,000 records.

**Source(s):** Anthropic code execution with MCP; MCP-Zero arXiv 2506.01056; MCP Workflow Engine arXiv 2605.00827.

---

## B. Domain examples and cases

### Case 1: Research assistant with too many connectors

A user connects Notion, Slack, Google Drive, GitHub, and web search. For a local chapter edit, most are irrelevant and increase tool-choice ambiguity.

### Case 2: Data audit

A database connector returns raw tables. A better server-side tool returns counts, anomalies, and a sample.

### Failure case: ambiguous tool overlap

Two servers both offer search. The agent spends turns choosing or uses the wrong one. Tool pruning reduces ambiguity.

---

## C. Connections and dependencies

**Prerequisites:**
- Chapter 5 fixed and connector cost.

**Unlocks:**
- Chapter 14 governance/security.
- Chapter 15 measurement of tool cost.

**Adjacent chapter connections:**
- Chapter 8: MCP configs vary by tool.
- Chapter 10: workflow patterns can isolate MCP-heavy research.

---

## D. Current state of the field

**Settled:**
- MCP is a major integration standard.
- Tool and payload design affect context efficiency.

**Contested or emerging:**
- Exact overhead numbers vary and should be labeled as measured examples, not universal constants.
- Best architecture for large MCP ecosystems is still changing.

**Key references:**
1. MCP lifecycle specification.
2. Anthropic, "Code execution with MCP."
3. MCP-Zero, arXiv 2506.01056.
4. "Separating Intelligence from Execution," arXiv 2605.00827.

**Recent developments:**
- Tool retrieval, workflow engines, and code-execution intermediaries are emerging as alternatives to naive schema injection.

---

## E. Teaching considerations

**Where students get stuck:**
- They do not know how many tools are active.
- They trust exact token figures from blog posts without measuring their own config.

**Analogies and framings that work:**
- MCP servers are power tools on the bench. Useful, but every plugged-in tool is also a hazard and a distraction.

**Exercises:**
- Inventory active MCP servers and classify each as always-needed, project-needed, or one-off.
- Rewrite one raw connector response into a token-efficient aggregate output.

---

## Local library cross-references

- `_lib_ai-claude-cowork-capabilities.md`
- `_lib_ai-claude-code-the-definitive-guide-to-agentic-development.md`

