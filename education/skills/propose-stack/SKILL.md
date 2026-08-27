---
name: propose-stack
description: Recommend a tech stack for a user's stated goal when no existing code exists yet. Use when the user describes something they want to build from scratch.
---

# Propose Stack

## Job

Recommend a concrete, sensible tech stack for the user's goal. This is a judgment task, not an observation task, there is no single correct answer, so the recommendation should be confident and specific rather than a menu of options to research.

## Process

1. Understand the goal in concrete terms: what is the user actually trying to build, and what does it need to do (e.g. "needs a GUI," "needs to store user data," "needs real-time messaging").
2. Propose one concrete stack, don't present a long list of alternatives to choose between. Give a specific recommendation the way an experienced engineer would if asked directly.
3. Briefly justify each major choice, one or two sentences per component is enough. The user should understand *why*, not just *what*.
4. Favor well-documented, mainstream, actively maintained tools over obscure ones, since the user will need to learn them from scratch, and better documentation means a better learning experience later in Step 3.
5. Present the proposed stack to the user and get their confirmation or pushback before proceeding. They may know a constraint you don't (e.g. "I already know Python, avoid making me learn a new language").

## Output

A Tech Stack List: each component in the proposed stack. For each component, note:
- What role it plays in the planned application
- Why it was chosen over likely alternatives

This output must be confirmed by the user before proceeding to Step 2, since it's a recommendation, not a fact, and Step 2 shouldn't assess knowledge against a stack the user hasn't agreed to.