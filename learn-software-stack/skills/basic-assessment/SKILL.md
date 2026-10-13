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

Ask as many questions as it takes to establish the user's knowledge. It's probably going to be close to the number of subjects/concepts/topics/tools in the tech stack, with a few more questions that narrow the understanding of the user.

## Output

A basic assessment of the user's skillset, relative to what would be necessary to complete the objectives of the proposed work on the project. 

Therefore, the List is now each subject/concept/topic/tool, plus a paragraph about how much it is used in the project, and another paragraph about how much the user knows about the subject.

## Your input files

The main agent gives you the path of the run folder. Read these files from it before you begin:
- `run.md`, for the **Goal** (the **project**) and any notes about this run.
- `01-tech-stack.md`, the Tech Stack List.

## Your output file

Write your output to `02-basic-assessment.md` in the run folder the main agent gave you.

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

After the header, write the content described below. Keep this file to that content. In `notes.md`, under the heading `## <step>, <agent>, round <N>` (leave out the round for a step that has none), list the files and sources you opened. For each choice in the output file, quote the evidence it rests on — a path and the passage you used, a source, or the user's words — and state what that evidence shows. Read `notes.md` only when the main agent's message tells you to.

Write the file so that an agent who has never seen this run could continue your step from the file alone.

Organize the file by subject, in the order of the Tech Stack List. Each subject gets one block: its heading, then each question you asked about it with the user's answer word for word, then the assessment described under *Output*. Number the questions in the order you asked them, across the whole interview. A question that covers several subjects goes in the block of the first subject it covers, and later blocks cite it by number. A subject you did not ask about gets a block with its assessment and the reason, for example "not asked: covered by item 5". Answers never go in a section apart from their subject.

Write a subject's heading, and each question and answer, into its block as soon as the answer arrives, before you ask the next question. Write the assessment when you finish the subject. The record then survives even if the run stops partway through.

After each answer, also append an entry to `notes.md` under your step's heading, labelled with the question number (for example "Q4"), holding in this order: the question, the user's answer word for word, the Tech Stack item the question checks, one sentence of what that answer shows about what the user knows (quote the words it comes from, as in "from this answer, the user can write a SELECT with a WHERE clause"), the assessment sentence you wrote for that item in the output file, and the next question. These entries stay out of the output file.

## Exits

- `DONE → User Interview`: the basic assessment of every item in the Tech Stack List is complete.

## Reporting back

You are working inside the `/curriculum` process. The main agent passes your messages on exactly as you write them, and it acts only on the marker that ends your turn. End every turn with exactly one of these markers, on its own line, followed by the content that goes with it:

- `ASK USER:` followed by one question or message for the user. The user's reply comes back to you.
- `ASK <agent-name>:` followed by a question for another agent in the process: `code-recon`, `stack-advisor`, `simple-interviewer`, `interviewer`, `deep-researcher`, `code-reader`, `tech-writer` or `skeptical-student`. Name the agent that owns the answer. The answering agent records its answer in its own output file and sends you that file's path. Read the file, then continue from where you stopped.
- `ANSWER: <path>` followed, on the next line, by a one-line summary. Use this to finish every exchange that began with a question to you. First record your answer in your own output file, in a new section that names who asked and what they asked. Before answering, you may ask the user or another agent for what you need.
- `DONE → <next state>: <path>` followed, on the next line, by a one-line summary. The path is the output file you wrote for this step. Choose the next state from the Exits above, or `END` when your Exits say the process is complete.

Write your file before you send `ANSWER` or `DONE`. The main agent checks that the file exists before passing anything on.
