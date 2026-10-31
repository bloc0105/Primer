---
name: review-product-changes
description: The "Review Product Changes" state of the /curriculum process, run by auditor. Load only when /curriculum has sent you into the "Review Product Changes" state.
user-invocable: false
---

# Review Product Changes

## Basics

- Performed by the `auditor` Agent.

## Input

- The Goal, in the user's words.
- The end-state, the tools and the change list.
- When there is a codebase: `current-code.md`.

## The Process

The `stack-advisor` decides what the product needs. The user can judge whether the end-state is what they want, but not whether a technical change is needed to reach it. You check that, so that nothing reaches the user, and nothing reaches the lessons, that the end-state doesn't need.

Check the list against each rule below. Each rule is a yes/no test. When the answer to any test is no, the list is not approved: list the failure as a finding that quotes the failing text and says why it fails.

1. Does the end-state name only outcomes the Goal asks for, or that the user asked for in a `product-changes-explained-r<N>.md`?
2. Does every change not marked **Recommended: security** name, in its `Needed for:` line, an outcome in the end-state?
3. For each of those changes, is that outcome impossible without the change, given what `current-code.md` shows the project already does? This is the core judgment of this state: for each change you fail, say what already makes the outcome possible, or why the outcome doesn't need it.
4. Is every change marked **Recommended: security** a vulnerability in what the end-state exposes, with one sentence saying what happens if it's left out, in terms of what someone could do or see? This is the only rule that checks a recommended change.
5. When the list is an amendment after a research finding: does it change the end-state?

Rule 5 doesn't fail a list. It decides your exit.

When the list was sent back to you after your findings, check each earlier finding against the new list, and check that nothing changed that your findings didn't name.

## Output

Approval, or the findings for the `stack-advisor`.

## Your input files

The main agent gives you the path of the run folder. Read these files from it before you begin:
- `run.md`, for the **Goal** (the **project**) and any notes about this run.
- The `product-changes-r<N>.md` with the highest round number, and the one before it when the list is a revision or an amendment.
- `current-code.md`, when there is a codebase.
- Every `product-changes-explained-r<N>.md`, if there are any, for the outcomes the user asked for.
- `basic-assessment.md`, when it exists, to choose your exit.
- `curriculum.md`, when the list is an amendment after a research finding, for the finding.
- Your earlier reviews, `review-product-changes-r*.md`, if there are any.

## Your output file

Write your output to `review-product-changes-r<N>.md` in the run folder the main agent gave you, with the same `<N>` as the list you review.

Start the file with this header:

```
---
state: Review Product Changes
agent: auditor
run: <run folder name>
inputs:
  - <each file you read>
---
```

After the header, write the content described below. Keep this file to that content. In `notes.md`, under the heading `## <state>, <agent>, round <N>` (leave out the round for a state that has none), list the files and sources you opened. For each choice in the output file, quote the evidence it rests on — a path and the passage you used, a source, or the user's words — and state what that evidence shows. Read `notes.md` only when the main agent's message tells you to.

Write the file so that an agent who has never seen this run could continue your work in this state from the file alone.

The file contains:
- Approval, or the list of findings.
- When the list was sent back after your findings: for each earlier finding, whether it was addressed.
- For an amendment: whether it changes the end-state.

## Exits

Take the first exit that matches.

1. `DONE → Define Product Changes`: there are findings. Send the path of your review.
2. `DONE → Confirm Product Changes`: the list is an approved amendment that leaves the end-state as it was, and a recommended change in it has no decision yet in any `product-changes-explained-r<N>.md`. This holds even when the amendment involves a tool or concept `basic-assessment.md` doesn't cover.
3. `DONE → Topic Research`: the list is an approved amendment that leaves the end-state as it was, and every recommended change in it has a decision. This holds even when the amendment involves a tool or concept `basic-assessment.md` doesn't cover.
4. `DONE → Basic Assessment`: any other approved list that involves a tool or concept `basic-assessment.md` doesn't cover yet, including when there is no `basic-assessment.md`.
5. `DONE → Confirm Product Changes`: any other approved list.

## Reporting back

You are working inside the `/curriculum` process. The main agent passes your messages on exactly as you write them, and it acts only on the marker that ends your turn. End every turn with exactly one of these markers, on its own line, followed by the content that goes with it:

- `ASK USER:` followed by one question or message for the user. The main agent shows it to the user and sends you their reply word for word. That reply is the user's answer: record it as theirs.
- `ASK <agent-name>:` followed by a question for another agent in the process: `code-recon`, `stack-advisor`, `auditor`, `simple-interviewer`, `interviewer`, `deep-researcher`, `code-reader`, `tech-writer` or `skeptical-student`. Name the agent that owns the answer. The answering agent records its answer in its own output file and sends you that file's path. Read the file, then continue from where you stopped.
- `ANSWER: <path>` followed, on the next line, by a one-line summary. Use this to finish every exchange that began with a question to you. First record your answer in your own output file, in a new section that names who asked and what they asked. Before answering, you may ask the user or another agent for what you need.
- `DONE → <next state>: <path>` followed, on the next line, by a one-line summary. The path is the output file you wrote in this state. Choose the next state from the Exits above, or `END` when your Exits say the process is complete.

Write your file before you send `ANSWER` or `DONE`. The main agent checks that the file exists before passing anything on.
