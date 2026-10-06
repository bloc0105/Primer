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

## Your input files

The main agent gives you the path of the run folder. Read these files from it before you begin:
- `run.md`, for the user's request (the **project**) and any notes about this run.
- `01-tech-stack.md`, `02-basic-assessment.md` and `03-interview.md`, for the project and the user's knowledge.
- `04-curriculum.md`, the curriculum.
- Every `05-code-review-*.md` file in the folder, if there are any.
- The lesson plan with the highest round number, `06-lesson-plan-r<N>.md`.
- Your earlier reviews, `07-review-r*.md`, if there are any. Check each earlier change-request against the new round, and check the **Changes made** list against what actually changed.

## Your output file

Write your output to `07-review-r<N>.md` in the run folder the main agent gave you. `<N>` is the round number of the lesson plan you are reviewing, so `07-review-r2.md` reviews `06-lesson-plan-r2.md`.

Start the file with this header:

```
---
step: Compare Curriculum to Task
agent: skeptical-student
run: <run folder name>
inputs:
  - <each file you read>
---
```

After the header, write the content described below. End the file with a `## How I got here` section that explains how you reached your conclusions: what you looked at, what you weighed, and why you decided as you did.

Write the file so that an agent who has never seen this run could continue your step from the file alone.

The file contains:
- Approval, or the list of change-requests, as described under *Output*.
- From round 2 on: for each change-request in your previous review, whether it was addressed.

## Exits

- `DONE → END`: you approve the lesson plan. Send the path of your review. Your one-line summary names the approved lesson plan file.
- `DONE → Write the Lesson Plan`: you withhold approval. Send the path of your review, which holds the change-requests for the `tech-writer`.

## Reporting back

You are working inside the `/curriculum` process. The main agent passes your messages on exactly as you write them, and it acts only on the marker that ends your turn. End every turn with exactly one of these markers, on its own line, followed by the content that goes with it:

- `ASK USER:` followed by one question or message for the user. The user's reply comes back to you.
- `ASK <agent-name>:` followed by a question for another agent in the process: `code-recon`, `stack-advisor`, `simple-interviewer`, `interviewer`, `deep-researcher`, `code-reader`, `tech-writer` or `skeptical-student`. Name the agent that owns the answer. The answering agent records its answer in its own output file and sends you that file's path. Read the file, then continue from where you stopped.
- `ANSWER: <path>` followed, on the next line, by a one-line summary. Use this to finish every exchange that began with a question to you. First record your answer in your own output file, in a new section that names who asked and what they asked. Before answering, you may ask the user or another agent for what you need.
- `DONE → <next state>: <path>` followed, on the next line, by a one-line summary. The path is the output file you wrote for this step. Choose the next state from the Exits above, or `END` when your Exits say the process is complete.

Write your file before you send `ANSWER` or `DONE`. The main agent checks that the file exists before passing anything on.
