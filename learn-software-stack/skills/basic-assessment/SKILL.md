---
name: basic-assessment
description: The "Basic Assessment" state of the /curriculum process. Load only when /curriculum has sent you into the "Basic Assessment" state.
user-invocable: false
---

# Basic Assessment

## Basics
- Performed by the `simple-interviewer` Agent.

## Input
The tools and concepts the change list involves.

## The Process

This is an informal assessment of the learner's skill level in the tools and concepts the changes involve. It's simply meant to establish the level of knowledge that the user feels they have about each one.

Ask as many questions as it takes to establish what the user knows of each tool and concept the changes involve, with a few more that narrow it down.

Ask about the tools and concepts, not about the changes. The changes are shown to the user in *Confirm Product Changes*.

When `basic-assessment.md` already exists, ask only about the tools and concepts it doesn't cover yet, and add their blocks to the end of the file. Leave the earlier blocks as they are.

## Output

A basic assessment of the user's skillset, relative to what the changes need.

For each tool or concept, a paragraph about how much the user knows of it.

## Your input files

The main agent gives you the path of the run folder. Read these files from it before you begin:
- `run.md`, for the **Goal** (the **project**) and any notes about this run.
- `product-changes-r<N>.md` with the highest round number, for its Tools list and its Involves lines.

## Your output file

Write your output to `basic-assessment.md` in the run folder the main agent gave you.

Start the file with this header:

```
---
state: Basic Assessment
agent: simple-interviewer
run: <run folder name>
inputs:
  - <each file you read>
---
```

After the header, write the content described below. Keep this file to that content. In `notes.md`, under the heading `## <state>, <agent>, round <N>` (leave out the round for a state that has none), list the files and sources you opened. For each choice in the output file, quote the evidence it rests on — a path and the passage you used, a source, or the user's words — and state what that evidence shows. Read `notes.md` only when the main agent's message tells you to.

Write the file so that an agent who has never seen this run could continue your work in this state from the file alone.

Organize the file by tool or concept, in the order the change list first names them. On a later pass, add the new blocks at the end, in the order the revised list first names them. Each one gets one block: its heading, then each question you asked about it with the user's answer word for word, then the assessment described under *Output*. Number the questions in the order you asked them, across the whole interview. A question that covers several tools or concepts goes in the block of the first one it covers, and later blocks cite it by number. A tool or concept you did not ask about gets a block with its assessment and the reason, for example "not asked: covered by item 5". Answers never go in a section apart from their tool or concept.

Write a tool or concept's heading, and each question and answer, into its block as soon as the answer arrives, before you ask the next question. Write the assessment when you finish it. The record then survives even if the run stops partway through.

After each answer, also append an entry to `notes.md` under your state's heading, labelled with the question number (for example "Q4"), holding in this order: the question, the user's answer word for word, the tool or concept the question checks, one sentence of what that answer shows about what the user knows (quote the words it comes from, as in "from this answer, the user can write a SELECT with a WHERE clause"), the assessment sentence you wrote for it in the output file, and the next question. These entries stay out of the output file.

## Exits

- `DONE → Confirm Product Changes`: the basic assessment of every tool and concept the changes involve is complete.

## Reporting back

You are working inside the `/curriculum` process. The main agent passes your messages on exactly as you write them, and it acts only on the marker that ends your turn. End every turn with exactly one of these markers, on its own line, followed by the content that goes with it:

- `ASK USER:` followed by one question or message for the user. The main agent shows it to the user and sends you their reply word for word. That reply is the user's answer: record it as theirs.
- `ASK <agent-name>:` followed by a question for another agent in the process: `code-recon`, `stack-advisor`, `auditor`, `simple-interviewer`, `interviewer`, `deep-researcher`, `code-reader`, `tech-writer` or `skeptical-student`. Name the agent that owns the answer. The answering agent records its answer in its own output file and sends you that file's path. Read the file, then continue from where you stopped.
- `ANSWER: <path>` followed, on the next line, by a one-line summary. Use this to finish every exchange that began with a question to you. First record your answer in your own output file, in a new section that names who asked and what they asked. Before answering, you may ask the user or another agent for what you need.
- `DONE → <next state>: <path>` followed, on the next line, by a one-line summary. The path is the output file you wrote in this state. Choose the next state from the Exits above, or `END` when your Exits say the process is complete.

Write your file before you send `ANSWER` or `DONE`. The main agent checks that the file exists before passing anything on.
