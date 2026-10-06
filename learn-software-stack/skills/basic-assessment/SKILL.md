---
name: basic-assessment
description: Step 2 of the /curriculum process ("Basic Assessment"). Load only when /curriculum has sent you into the "Basic Assessment" state.
user-invocable: false
---

# Basic Assessment

## Basics
- Performed by the `simple-interviewer` Agent.

## Input
The Tech Stack List from the Task Analysis

## The Process

This is an informal assessment of the skill level on the tech stack of the learner. It's simply meant to establish the level of knowledge that the user feels they have about a subject. 

## Output

A basic assessment of the user's skillset, relative to what would be necessary to complete the objectives of the proposed work on the project. 

Therefore, the List is now each subject/concept/topic/tool, plus a paragraph about how much it is used in the project, and another paragraph about how much the user knows about the subject.

## Your input files

The main agent gives you the path of the run folder. Read these files from it before you begin:
- `run.md`, for the user's request (the **project**) and any notes about this run.
- `01-tech-stack.md`, the Tech Stack List.

## Your output file

Write your output to `02-basic-assessment.md` in the run folder the main agent gave you. Add each question and the user's answer to the file as soon as the answer arrives, before you ask the next question, so the record survives even if the run stops partway through.

Start the file with this header:

```
---
step: Basic Assessment
agent: simple-interviewer
run: <run folder name>
inputs:
  - <each file you read>
---
```

After the header, write the content described below. Do not put your reasoning in this file. Append it to `notes.md` in the run folder, under the heading `## <step>, <agent>, round <N>` (leave out the round for a step that has none), covering what you looked at, what you weighed, and why you decided as you did. Read `notes.md` only when the main agent's message tells you to.

Write the file so that an agent who has never seen this run could continue your step from the file alone.

The file contains:
- Every question you asked, and the user's answer, word for word, in order.
- The assessment described under *Output*.

## Exits

- `DONE → User Interview`: the basic assessment of every item in the Tech Stack List is complete.

## Reporting back

You are working inside the `/curriculum` process. The main agent passes your messages on exactly as you write them, and it acts only on the marker that ends your turn. End every turn with exactly one of these markers, on its own line, followed by the content that goes with it:

- `ASK USER:` followed by one question or message for the user. The user's reply comes back to you.
- `ASK <agent-name>:` followed by a question for another agent in the process: `code-recon`, `stack-advisor`, `simple-interviewer`, `interviewer`, `deep-researcher`, `code-reader`, `tech-writer` or `skeptical-student`. Name the agent that owns the answer. The answering agent records its answer in its own output file and sends you that file's path. Read the file, then continue from where you stopped.
- `ANSWER: <path>` followed, on the next line, by a one-line summary. Use this to finish every exchange that began with a question to you. First record your answer in your own output file, in a new section that names who asked and what they asked. Before answering, you may ask the user or another agent for what you need.
- `DONE → <next state>: <path>` followed, on the next line, by a one-line summary. The path is the output file you wrote for this step. Choose the next state from the Exits above, or `END` when your Exits say the process is complete.

Write your file before you send `ANSWER` or `DONE`. The main agent checks that the file exists before passing anything on.
