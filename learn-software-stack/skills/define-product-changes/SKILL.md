---
name: define-product-changes
description: The "Define Product Changes" state of the /curriculum process, run by stack-advisor. Load only when /curriculum has sent you into the "Define Product Changes" state.
user-invocable: false
---

# Define Product Changes

## Basics

- Performed by the `stack-advisor` Agent.

## Input

- The Goal, in the user's words.
- When there is a codebase: `current-code.md`, and the code itself.
- When the user has rejected a list: that list, and the user's words rejecting it.
- When research found that an accepted change needs more work: the accepted list, and the researcher's finding in `curriculum.md`.

## The Process

The user can state what they want, but not the work that would get them there. You determine that work. Everything after this state serves it, and nothing after it can add to it.

Write the list the way you would write a plan for making these changes yourself: file by file, what each part does now and what it must do instead. Stop before the code. The user makes these changes, during the lessons.

**The end-state.** Describe the finished product: what it does when the Goal is reached. Draw it from the Goal and, when there is a codebase, from what the project already is. Name only outcomes the user asked for.

**The tools.** When there is no codebase, choose the tools the changes need: one concrete choice for each need, mainstream and well documented. When there is a codebase, use what it already uses, and add a tool only when no existing one can do the job.

**The change list.** The changes that reach the end-state. Each change says what the project does now, where, and what it does instead, and lists the tools and concepts it involves. Read the code before you name a file or area. When there is no codebase, the areas are the ones the end-state will need. Don't write the new code; the user writes it during the lessons.

Keep a change only when the end-state is impossible without it. A change that is usual, that makes the product feel complete, that a tutorial starts with, or that only improves how the code looks, stays off the list. A problem in `current-code.md` goes on the list only when the end-state is impossible without fixing it.

A vulnerability in what the end-state exposes, such as a secret stored or sent unprotected, goes on the list as a recommended change, marked **Recommended: security**, with one sentence saying what it protects against. The user keeps or drops it in *Confirm Product Changes*.

When revising a rejected list, change only what the user's words ask for, and leave every other change as it was. When amending a list after a research finding, amend only what the finding requires.

## Output

The end-state, the tools, and the change list.

## Your input files

The main agent gives you the path of the run folder. Read these files from it before you begin:
- `run.md`, for the **Goal** (the **project**) and any notes about this run.
- `current-code.md`, when there is a codebase.
- `basic-assessment.md`, when it exists, to choose your exit.
- When the user has rejected a list, or research found that an accepted change needs more work: the `product-changes-r<N>.md` and `product-changes-explained-r<N>.md` with the highest round number.
- When research found that an accepted change needs more work: `curriculum.md`, for the finding.

## Your output file

Write your output to `product-changes-r<N>.md` in the run folder the main agent gave you. `<N>` is 1 for the first list, and one more than the highest existing round for a revised list. Leave earlier rounds as they are.

Start the file with this header:

```
---
state: Define Product Changes
agent: stack-advisor
run: <run folder name>
inputs:
  - <each file you read>
---
```

After the header, write the content described below. Keep this file to that content. In `notes.md`, under the heading `## <state>, <agent>, round <N>` (leave out the round for a state that has none), list the files and sources you opened. For each choice in the output file, quote the evidence it rests on — a path and the passage you used, a source, or the user's words — and state what that evidence shows. For each change, also say why the end-state is impossible without it. Read `notes.md` only when the main agent's message tells you to.

Write the file so that an agent who has never seen this run could continue your work in this state from the file alone.

The file contains:
- **End-state:** the description of the finished product.
- **Tools:** each tool the changes involve, with its version, and for a new tool one sentence on why it was chosen.
- **Changes:** one item per change, in this form:

  ```
  Currently <what the project does now>, in <the file or area where it is>. Make it so that <what it does instead>.
  - Involves: <tools and concepts>
  ```

## Exits

- `DONE → Basic Assessment`: the list involves a tool or concept `basic-assessment.md` doesn't cover yet, including when there is no `basic-assessment.md`.
- `DONE → Confirm Product Changes`: `basic-assessment.md` covers every tool and concept the list involves.

## Reporting back

You are working inside the `/curriculum` process. The main agent passes your messages on exactly as you write them, and it acts only on the marker that ends your turn. End every turn with exactly one of these markers, on its own line, followed by the content that goes with it:

- `ASK USER:` followed by one question or message for the user. The main agent shows it to the user and sends you their reply word for word. That reply is the user's answer: record it as theirs.
- `ASK <agent-name>:` followed by a question for another agent in the process: `code-recon`, `stack-advisor`, `simple-interviewer`, `interviewer`, `deep-researcher`, `code-reader`, `tech-writer` or `skeptical-student`. Name the agent that owns the answer. The answering agent records its answer in its own output file and sends you that file's path. Read the file, then continue from where you stopped.
- `ANSWER: <path>` followed, on the next line, by a one-line summary. Use this to finish every exchange that began with a question to you. First record your answer in your own output file, in a new section that names who asked and what they asked. Before answering, you may ask the user or another agent for what you need.
- `DONE → <next state>: <path>` followed, on the next line, by a one-line summary. The path is the output file you wrote in this state. Choose the next state from the Exits above, or `END` when your Exits say the process is complete.

Write your file before you send `ANSWER` or `DONE`. The main agent checks that the file exists before passing anything on.
