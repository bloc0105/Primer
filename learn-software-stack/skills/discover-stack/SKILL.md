---
name: discover-stack
description: Step 1 of the /curriculum process ("Task Analysis", Discovery Mode), run by code-recon. Trace an existing codebase to determine its actual tech stack.
user-invocable: false
---

# Discover Stack

## Job

Read the codebase and report, as fact, what it's actually built with. This is an observation task, not a recommendation task: report facts, including when a pattern is objectively wrong, deprecated, or buggy — that's still something that's there, not a suggestion. What's off-limits is proposing the fix: do not suggest alternatives, redesigns, or how something should have been done instead.

## Process

1. If the user named a specific bug, feature, or file, scope the trace to the subsystem that touches it, don't map the entire codebase if only a small piece of it is relevant. If the user wants to understand the whole codebase, map it in full.
2. Trace actual imports, dependencies, build files, and package manifests, don't infer from the project's name or description alone, read the real files.
3. Identify every language, framework, library, and external tool involved in the scoped area.
4. Note anything unusual: obscure or undocumented internal tools, deprecated or unusual versions, custom forks. Flag these explicitly, since they may be harder to find standard documentation for.

## Output

A Tech Stack List: each component the user would need to know to work on this scoped part of the codebase. For each component, note:
- What it's used for in this codebase specifically (not generically)
- Whether it's mainstream/well-documented or obscure/custom
- Roughly how deep the codebase's usage of it goes (e.g. "uses one basic API call" vs. "relies on advanced features throughout")

## Output for /curriculum

The output of the initial assessment should be the **Tech Stack list.**  This is the list of subject/concept/topic/tools that are used in the project.  Each subject/concept/topic/tool should be listed, followed by a brief paragraph describing how that tool is used in the project.

## Exits

- `DONE → Basic Assessment`: the Tech Stack List is complete.

## Reporting back

You are working inside the `/curriculum` process. The main agent passes your messages on exactly as you write them, and it acts only on the marker that ends your turn. End every turn with exactly one of these markers, on its own line, followed by the content that goes with it:

- `ASK USER:` followed by one question or message for the user. The user's reply comes back to you.
- `ASK <agent-name>:` followed by a question for another agent in the process: `code-recon`, `stack-advisor`, `simple-interviewer`, `interviewer`, `deep-researcher`, `code-reader`, `tech-writer` or `skeptical-student`. Name the agent that owns the answer. Its answer comes back to you, and you continue from where you stopped.
- `ANSWER:` followed by your reply to a question another agent asked you. Finish every exchange that began with a question to you this way. Before answering, you may ask the user or another agent for what you need.
- `DONE → <next state>:` followed by the finished output of your step. Choose the next state from the Exits above, or `END` when your Exits say the process is complete.
