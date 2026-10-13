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

The task is to check the work of the lesson plan against each rule below. Each rule is a yes/no test. When the answer to any test is no, withhold approval and list the failure as a change-request that quotes the failing text. A plan that fails a rule is not approved, and no failure is excused as acceptable, minor, or fine here. When you believe a rule should not apply, end your turn with `ASK USER:` naming the rule, quoting the failing text, and giving your reason. The plan stays unapproved until the user answers, and you record their answer in your review.

**Rules:**
1. Does every unit have Vocabulary, Reading and Practical sub-sections, in that order? (Vocabulary and Reading may state that none are needed.)
2. Does every Vocabulary and Reading item depend only on knowledge taught earlier in the plan?
3. Does every practical name a concept from its own unit's Vocabulary or Reading sub-section?
4. Does every practical (Unit 0 excepted) name the file or area of the project where the work happens and state a change to make there?
5. Does every practical state a result the learner can observe, and how to observe it?
6. Is every practical's completion independent of any written output (a note, list, explanation, prediction or decision)?
7. Does every practical avoid creating a scratch file, folder or throwaway edit?
8. Does every practical use only concepts taught earlier, apart from later-unit code that the step names, with the unit, where the code appears?
9. Does the plan begin with a unit whose practical is running the project unchanged, with setup steps included if and only if the interview assessment shows the user cannot run it already?
10. Does every reading item that lists several sections name the parent section first, link to it, and then list the subsections to read?
11. Does every reading item name what to read by section number or heading, without describing how the page looks (a box, a sidebar, a table)?
12. Is every term in an assigned reading that the learner needs defined in this unit's Vocabulary or an earlier unit's, or marked in its citation as safe to ignore?
13. Does the plan pass each voice rule stated in the lesson-plan writing instructions? Search the plan file for each one.
14. Is every Vocabulary and Reading item one citation, with at most one sentence of the plan's own words?
15. Is every Vocabulary and Reading sub-section free of any code, definition or analogy the plan wrote, apart from correction notes of two sentences or fewer that name the section they correct?
16. Is every Vocabulary definition verbatim from its cited source? Fetch the page to check.
17. From round 2: was each of your earlier change-requests addressed, and does the plan change nothing you did not ask for?

**Judgment checks:** some qualities can't be made yes/no. For each of these, make a finding when you judge it fails, label it `[judgment]`, and say why: whether each practical moves the project toward the Goal (the writer records the intended link in its `notes.md` entry), whether each practical suits the user's knowledge level, whether any item is worded incorrectly, whether each correction note fixes something the cited documentation really gets wrong or omits, whether any Vocabulary list is too long to read before its unit, and any judgment checks in your own guidelines. Apply the split-attention check in your guidelines to the Practical sub-sections, which are the plan's own writing.

This agent has no shell or git access — if verifying sufficiency requires checking the user's own project source, that source must already be materialized as plain, readable files (see *Topic Code Review*) before this agent is invoked.

## Output

Final approval on the curriculum for the user to follow, or — if approval is withheld — a set of change-requests sent back to whoever owns the affected content. This can go through multiple iterations, but if every rule passes and every change-request was addressed, approve.  But don't let the writer get away with changing things that you didn't tell it to, and sneaking in new problems.

## Your input files

The main agent gives you the path of the run folder. Read these files from it before you begin:
- `run.md`, for the **Goal** (the **project**) and any notes about this run.
- `01-tech-stack.md`, `02-basic-assessment.md` and `03-interview.md`, for the project and the user's knowledge.
- `04-curriculum.md`, the curriculum.
- Every `05-code-review-*.md` file in the folder, if there are any.
- The lesson plan with the highest round number, `06-lesson-plan-r<N>.md`.
- Your earlier reviews, `07-review-r*.md`, if there are any. Check each earlier change-request against the new round, and check the **Changes made** list against what actually changed. The list is in the tech-writer's entry for the previous round in `notes.md`; read that entry.

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

After the header, write the content described below. Keep this file to that content. In `notes.md`, under the heading `## <step>, <agent>, round <N>` (leave out the round for a step that has none), list the files and sources you opened. For each choice in the output file, quote the evidence it rests on — a path and the passage you used, a source, or the user's words — and state what that evidence shows. Read `notes.md` only when the main agent's message tells you to.

Write the file so that an agent who has never seen this run could continue your step from the file alone.

The file contains:
- Approval, or the list of change-requests, as described under *Output*.
- From round 2 on: for each change-request in your previous review, whether it was addressed.
- The user's answer to each exception you asked about.

## Exits

- `ASK USER`: you want to propose an exception to a rule, as described under *The Process*.
- `DONE → END`: you approve the lesson plan. Send the path of your review. Your one-line summary names the approved lesson plan file.
- `DONE → Write the Lesson Plan`: you withhold approval. Send the path of your review, which holds the change-requests for the `tech-writer`.

## Reporting back

You are working inside the `/curriculum` process. The main agent passes your messages on exactly as you write them, and it acts only on the marker that ends your turn. End every turn with exactly one of these markers, on its own line, followed by the content that goes with it:

- `ASK USER:` followed by one question or message for the user. The user's reply comes back to you.
- `ASK <agent-name>:` followed by a question for another agent in the process: `code-recon`, `stack-advisor`, `simple-interviewer`, `interviewer`, `deep-researcher`, `code-reader`, `tech-writer` or `skeptical-student`. Name the agent that owns the answer. The answering agent records its answer in its own output file and sends you that file's path. Read the file, then continue from where you stopped.
- `ANSWER: <path>` followed, on the next line, by a one-line summary. Use this to finish every exchange that began with a question to you. First record your answer in your own output file, in a new section that names who asked and what they asked. Before answering, you may ask the user or another agent for what you need.
- `DONE → <next state>: <path>` followed, on the next line, by a one-line summary. The path is the output file you wrote for this step. Choose the next state from the Exits above, or `END` when your Exits say the process is complete.

Write your file before you send `ANSWER` or `DONE`. The main agent checks that the file exists before passing anything on.
