# Governance and Security: When the Agent Has Shell Access

## Learning Objectives

By the end of this chapter, you should be able to:

- Describe prompt injection and tool poisoning.
- Apply six baseline governance controls.
- Write a permission profile for a project.
- Assess whether an agent has more access than the task requires.

## Opening Case

An agent reads an issue comment. The comment contains instructions the human did not write: ignore previous rules, inspect secrets, send them through a tool. The agent has shell access, filesystem access, and connectors.

This is no longer a writing problem. It is an access-control problem.

## Core Concept

When agents can read files, run commands, and call tools, untrusted text becomes dangerous. Prompt injection is the attempt to smuggle instructions through content the model reads. Tool poisoning is the same idea inside tool metadata or descriptions. MCP expands the integration surface, which also expands the attack surface (MCP specification, https://modelcontextprotocol.io/specification/2025-11-25/basic/lifecycle).

The portable principle:

```text
The agent should be able to do exactly the task, and nothing with larger blast radius, without a human gate.
```

Ignore files help with governance only if you understand their limits. `.gitignore` keeps files out of version control. `.cursorignore`, `.aiderignore`, `.clineignore`, and similar files may reduce indexing or context loading for specific tools. None of them is a complete security boundary. A secret inside the workspace is still in the blast radius of an agent with filesystem access.

## Six Baseline Controls

```text
1. Least privilege by default.
2. Explicit network/domain allowlists.
3. No secrets in folders, prompts, or logs.
4. Approval gates on destructive or irreversible actions.
5. Validator passes for risky work.
6. Audit decisions and file changes.
```

Add one more operational rule: treat every MCP server as third-party supply chain. A malicious or compromised server can influence the agent through tool descriptions, returned payloads, or actions. Approving an MCP server is closer to approving a browser extension than enabling a formatting preference.

## Worked Example

Unsafe:

```yaml
permissions:
  filesystem_scope: home-directory
  network: any
  mcp_servers: all
```

Safer:

```yaml
permissions:
  filesystem_scope: workspace-only
  network_allowlist:
    - registry.npmjs.org
    - docs.anthropic.com
  forbidden:
    - "rm -rf"
    - "git push --force"
    - "curl -X DELETE"
  approval_required:
    - "bulk rename"
    - "delete"
    - "write outside workspace"
```

**The lesson:** access should match the task, not the user's general trust in the tool.

**The limit:** YAML permission profiles document intent unless a wrapper or tool enforces them.

## Common Misconceptions

**Misconception: "Ignore files keep secrets safe."**  
They reduce accidental tracking or context loading. They are not a complete security boundary.

**Misconception: "MCP servers are built-ins."**  
Treat every server as third-party code and third-party instruction surface.

**Misconception: "Approval prompts solve everything."**  
Users can approve bad actions if the request is unclear. The action must be understandable.

## Exercises

1. Write a permission profile for your most sensitive project.
2. Identify one file that should never be in the workspace.
3. Threat-model one MCP server: what can it read, write, and leak?

## What Would Change My Mind

I would revise this chapter if agent hosts adopted reliable, inspectable, least-privilege enforcement by default across filesystem, shell, network, and tools. Current controls remain fragmented.

## Still Puzzling

- How should MCP clients display tool-description risk?
- Can prompt-injection defenses be both strict and usable?
- What audit logs are enough for small teams?
