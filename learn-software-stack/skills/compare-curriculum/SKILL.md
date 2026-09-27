---
name: compare-curriculum
description: Step 7 of the /curriculum process ("Compare Curriculum to Task"). Load only when /curriculum has sent you into the "Compare Curriculum to Task" state.
user-invocable: false
---

# Compare Curriculum to Task

## Basics

- Performed by the `skeptical-student` Agent.

## Input

The lesson plan that was written.

## The Process

The task is to check the work of the lesson plan. They are looking to make sure that each section has both a documentation sub-section and a practical sub-section. 


There shall be a check of the documentation sub-section. They are checking for things that are ordered incorrectly, as in things that have pre-requisite knowledge out of order. Or things that are worded incorrectly.  

In addition, for every lesson, read the practical portion and consider the following:
- Does this apply the lessons learned from the documentation?
- Does this move the project forward?
- Is this appropriate to the user's knowledge level?

This agent has no shell or git access — if verifying sufficiency requires checking the user's own project source, that source must already be materialized as plain, readable files (see *Topic Code Review*) before this agent is invoked.

## Output

Final approval on the curriculum for the user to follow, or — if approval is withheld — a set of change-requests sent back to whoever owns the affected content. This can go through multiple iterations, but if everything was addressed after review, you should approve.  But don't let the writer get away with changing things that you didn't tell it to, and sneaking in new problems.

## Exits

- `DONE → END`: you approve the lesson plan. The main agent shows your output to the user as the final curriculum, so include the approved lesson plan in full.
- `DONE → Write the Lesson Plan`: you withhold approval. Send your change-requests to the `tech-writer`.

## Reporting back

You are working inside the `/curriculum` process. The main agent passes your messages on exactly as you write them, and it acts only on the marker that ends your turn. End every turn with exactly one of these markers, on its own line, followed by the content that goes with it:

- `ASK USER:` followed by one question or message for the user. The user's reply comes back to you.
- `ASK <agent-name>:` followed by a question for another agent in the process: `code-recon`, `stack-advisor`, `simple-interviewer`, `interviewer`, `deep-researcher`, `code-reader`, `tech-writer` or `skeptical-student`. Name the agent that owns the answer. Its answer comes back to you, and you continue from where you stopped.
- `ANSWER:` followed by your reply to a question another agent asked you. Finish every exchange that began with a question to you this way. Before answering, you may ask the user or another agent for what you need.
- `DONE → <next state>:` followed by the finished output of your step. Choose the next state from the Exits above, or `END` when your Exits say the process is complete.
