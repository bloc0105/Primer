---
name: discover-stack
description: Trace an existing codebase to determine its actual tech stack. Use when the user references existing code, a repo, a file path, or a specific bug they want to fix or understand.
---

# Discover Stack

## Job

Read the codebase and report, as fact, what it's actually built with. This is an observation task, not a recommendation task. Do not suggest alternatives or improvements, only report what is there.

## Process

1. If the user named a specific bug, feature, or file, scope the trace to the subsystem that touches it, don't map the entire codebase if only a small piece of it is relevant. If the user wants to understand the whole codebase, map it in full.
2. Trace actual imports, dependencies, build files, and package manifests, don't infer from the project's name or description alone, read the real files.
3. Identify every language, framework, library, and external tool involved in the scoped area.
4. Note anything unusual: obscure or undocumented internal tools, deprecated or unusual versions, custom forks. Flag these explicitly, since they may be harder to find documentation for in Step 3.

## Output

A Tech Stack List: each component the user would need to know to work on this scoped part of the codebase. For each component, note:
- What it's used for in this codebase specifically (not generically)
- Whether it's mainstream/well-documented or obscure/custom
- Roughly how deep the codebase's usage of it goes (e.g. "uses one basic API call" vs. "relies on advanced features throughout")

Do not proceed until this list is complete. This output feeds directly into Step 2 without requiring user confirmation, since it's a factual report, not a decision.