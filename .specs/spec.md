# Documentation Freshness & Verification Spec

## Purpose

This specification defines **how and when an agent MUST read the latest documentation** before performing any task that depends on external systems, APIs, tools, protocols, or standards.

This file is the **single source of truth** for documentation freshness rules. Agents must not invent, infer, or rely on outdated knowledge when this spec applies.

---

## Core Principle

> **Correctness > Speed > Convenience**

An agent is considered **non-compliant** if it executes reasoning or produces output based on assumptions that are not verified against the latest documentation.

---

## Mandatory Read Rule (MRR)

An agent **MUST read the latest documentation** if **any** of the following conditions are true:

* The task involves:

  * External APIs
  * SDKs / libraries
  * Frameworks
  * Cloud services
  * Security mechanisms
  * Configuration formats
* The version of the dependency is **not explicitly pinned**
* The dependency is known to evolve rapidly
* The output has **production, security, or financial impact**

If none of the above apply, documentation reading is OPTIONAL.

---

## What Counts as “Latest Documentation”

The agent must prefer documentation sources in the following order:

1. Official documentation website
2. Official GitHub repository (README / docs folder)
3. Official changelog or release notes
4. MCP-exposed documentation endpoints (if available)

Third-party blogs, tutorials, or StackOverflow answers **MUST NOT** be treated as authoritative.

---

## Documentation Verification Workflow

Before executing a task, the agent MUST follow this sequence:

```
1. Identify dependency
2. Check if version is pinned
3. If not pinned → read latest docs
4. Extract relevant constraints
5. Validate assumptions
6. Proceed with task
```

Skipping any step invalidates the output.

---

## Required Outputs After Reading Docs

After reading documentation, the agent MUST internally confirm:

* API names are correct
* Parameters and defaults are current
* Deprecated features are avoided
* Breaking changes are acknowledged

If uncertainty remains, the agent MUST:

* Ask for clarification, or
* Explicitly state uncertainty and limit scope

---

## MCP Integration Rule

If documentation access is provided via an MCP server:

* The agent MUST use the MCP capability instead of browsing
* The MCP result overrides any internal knowledge

Example valid skills:

* `docs.fetch_latest`
* `github.read_file`

---

## Caching & Reuse Policy

Agents MAY cache documentation results **only if**:

* The documentation explicitly declares a version
* The version is referenced in the output
* The cache lifetime is defined

Otherwise, documentation MUST be re-read per session.

---

## Failure & Refusal Conditions

The agent MUST refuse to proceed if:

* Documentation cannot be accessed
* Documentation is contradictory or incomplete
* Required permissions to read docs are missing

Refusal message MUST include:

* What documentation is missing
* Why it is required

---

## Anti-Patterns (Strictly Forbidden)

❌ Relying on model training knowledge
❌ Guessing undocumented behavior
❌ Using outdated examples
❌ Assuming backward compatibility

---

## Compliance Statement (Agent-Internal)

Before final output, the agent MUST internally validate:

> “This response complies with the Documentation Freshness & Verification Spec.”

If this statement cannot be truthfully made, the agent MUST halt.

---

## Why This Spec Exists

This spec exists to:

* Eliminate hallucinations
* Prevent silent breaking changes
* Enforce professional-grade outputs
* Align agent behavior with real-world engineering standards

---

**End of Spec**
