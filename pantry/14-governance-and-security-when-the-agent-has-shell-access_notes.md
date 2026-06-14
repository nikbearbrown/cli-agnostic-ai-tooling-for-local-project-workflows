# Research Notes: Chapter 14 - Governance and Security: When the Agent Has Shell Access

**Source:** TIKTOC.md chapter entry
**Notes file:** 14-governance-and-security-when-the-agent-has-shell-access_notes.md
**Corresponding chapter:** chapters/14-governance-and-security-when-the-agent-has-shell-access.md (not yet written)
**Generated:** 2026-06-14

---

## Chapter summary from TIKTOC.md

When agents have filesystem, shell, and MCP access, folder conventions are not enough. The chapter covers prompt injection, tool poisoning, least privilege, network allowlists, secrets, approval gates, validator passes, and audit logs.

---

## A. Conceptual foundations

### Prompt injection

Prompt injection exploits the model's difficulty separating trusted instructions from untrusted content. In agent workflows, untrusted content may be files, web pages, issue comments, logs, emails, or tool outputs.

**Common misconception:** "Prompt injection is only a chatbot trick." It matters more when the agent can call tools or edit files.

**Worked example:** A README from an untrusted repo contains hidden instructions to exfiltrate `.env`. The agent reads it during analysis.

**Source(s):** Prompt injection literature; Wired overview; OWASP LLM concerns; security papers.

### Tool poisoning and MCP-specific risk

MCP tool poisoning embeds malicious instructions in tool descriptions or metadata visible to the model. Recent papers identify tool poisoning, shadowing, and rug-pull variants as serious risks.

**Common misconception:** "A tool description is harmless documentation." For an LLM, tool descriptions are instructions in context.

**Worked example:** Malicious tool description says to call another tool and leak data while appearing to perform a normal task.

**Source(s):** "Model Context Protocol Threat Modeling..." arXiv 2603.22489; "Securing MCP..." arXiv 2512.06556; MCPTox arXiv 2508.14925.

### Least privilege as the portable principle

The agent should have exactly the access needed for the task and no larger blast radius without human approval. This applies to filesystem scope, shell commands, network, MCP servers, and secrets.

**Common misconception:** "More access means better agent." More access means more possible damage and more context ambiguity.

**Worked example:** A chapter research task needs web search and `pantry/` writes; it does not need access to private credentials or production deploy commands.

**Source(s):** General security principle; Claude hooks/permissions docs; MCP security papers.

---

## B. Domain examples and cases

### Case 1: Shell access in a repo

Agent can run `rm`, `mv`, `git`, package managers, and network commands. Controls: no-delete hook, approval for destructive commands, branch/worktree isolation.

### Case 2: MCP with private data

Slack/Drive/DB MCP servers can expose sensitive records. Controls: scoped servers, audit logs, allowlists, and clean-context validator.

### Failure case: secrets in folder

`.env` is gitignored but present. Agent reads it during broad search. Mitigation: keep secrets outside workspace and enforce read blocks where possible.

---

## C. Connections and dependencies

**Prerequisites:**
- Chapter 9 MCP cost.
- Chapter 11 file safety.

**Unlocks:**
- Chapter 15 measurement of risk and effectiveness.

**Adjacent chapter connections:**
- Chapter 13: failure catalog.
- Chapter 15: measuring whether controls work.

---

## D. Current state of the field

**Settled:**
- Prompt injection is a real class of LLM application risk.
- MCP expands the tool and data attack surface.
- Least privilege and approval gates are necessary baseline controls.

**Contested or emerging:**
- MCP security is evolving quickly; protocol-level mitigations are actively researched.
- Client defenses vary widely.

**Key references:**
1. MCP lifecycle specification.
2. arXiv 2603.22489, MCP threat modeling and tool poisoning.
3. arXiv 2512.06556, securing MCP against tool poisoning.
4. arXiv 2508.14925, MCPTox benchmark.
5. Claude hooks docs.

**Recent developments:**
- 2025-2026 research shifted attention from ordinary prompt injection to tool metadata, tool shadowing, and MCP supply-chain risk.

---

## E. Teaching considerations

**Where students get stuck:**
- They treat ignore files as security.
- They give blanket network/shell access because approvals are annoying.

**Analogies and framings that work:**
- The agent is an intern with a badge and a robot arm. It needs a job-specific badge, not master keys.

**Exercises:**
- Write a permissions block for a real project.
- Threat-model one MCP server: data it can access, actions it can take, worst plausible misuse.

---

## Local library cross-references

- `_lib_ai-claude-cowork-capabilities.md`
- `_lib_ai-software-engineering-at-google-lessons-learned-from-programming-over-time.md`

