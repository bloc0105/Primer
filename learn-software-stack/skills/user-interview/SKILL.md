---
name: user-interview
description: Step 3 of the /curriculum process ("User Interview"). Load only when /curriculum has sent you into the "User Interview" state.
user-invocable: false
---

# User Interview

## Basics
- Performed by the `interviewer` Agent.

## Input
The Basic Assessment of the learner's skill-set, plus the topic you were asked about and the sentence or section that needs it.

## The Process

The purpose of the basic assessment was to determine roughly what the user knows about a subject. Now is the point to narrow that understanding with precision, one topic at a time.

The `deep-researcher` sends you one topic at a time. Establish what the learner specifically knows about it, using what the basic assessment and earlier answers already show before you ask anything new. For instance, if the user explicitly said they know nothing about a certain subject/concept/topic/tool, it's probably not necessary to ask them about it. Ask as many questions as that takes. You are invoked one question per turn. Each turn you ask the user one question, and the next turn begins with the user's answer.

A turn may contain several asks only when every ask is labelled (a), (b), (c) and the labelled list is the last thing in the turn. An unlabelled sentence in a turn never asks for a response. Test: every sentence of the turn that asks for a response is one of the labelled asks.

You choose what to ask, interpret each answer, and decide when you can state what the learner knows about the topic. No other agent does. The researcher decides which topic comes next. You produce each determination yourself, from having tracked the interview throughout, and not by reconstructing it afterward.

Each topic comes with the sentence or section that needs it, so its bearing on the project is already established. To anchor a question in what the codebase actually does, ask `code-recon`.

## Output

For each topic, a statement of what the learner specifically can and can't do or say about it, with the evidence: their own words where possible, and for each gap, what the question needed that they lacked. There are no fixed categories. The user's conceptual knowledge will be separate from their vocabulary knowledge.  This means that if a user knows how to do something, but doesn't know the terminology for it, this is considered different from actually not knowing the subject/concept/tool/topic.  From this, the researcher can tell whether to stop on the topic or go further back.

## Your input files

The main agent gives you the path of the run folder. Read these files from it before you begin:
- `run.md`, for the **Goal** (the **project**) and any notes about this run.
- `01-tech-stack.md`, the Tech Stack List.
- `02-basic-assessment.md`, the basic assessment.
- `03-interview.md`, if it already exists. It holds the interview so far, and you continue from it: build on its questions, answers and assessment as your own.

## Your output file

Write your output to `03-interview.md` in the run folder the main agent gave you.

Start the file with this header:

```
---
step: User Interview
agent: interviewer
run: <run folder name>
inputs:
  - <each file you read>
---
```

After the header, write the content described below. Keep this file to that content. In `notes.md`, under the heading `## <step>, <agent>, round <N>` (leave out the round for a step that has none), list the files and sources you opened. For each choice in the output file, quote the evidence it rests on — a path and the passage you used, a source, or the user's words — and state what that evidence shows. Read `notes.md` only when the main agent's message tells you to.

Write the file so that an agent who has never seen this run could continue your step from the file alone.

Organize the file by topic, in the order the topics were asked. Each topic gets one block: its heading, who asked and the sentence or section that needs it, then each question you asked about it with the user's answer word for word, then the statement described under *Output*, with concept knowledge and vocabulary kept separate. Number the questions in the order you asked them, across the whole interview. A topic you answered from earlier evidence without asking gets a block with its statement and the evidence. Answers never go in a section apart from their topic. Add each new block to the end of the file, and keep everything above it exactly as it was.

Write a topic's heading, and each question and answer, into its block as soon as the answer arrives, before you ask the next question. The record then survives even if the run stops partway through.

After each answer, also append an entry to `notes.md` under your step's heading, labelled with the question number (for example "Q4"), holding in this order: the question, the user's answer word for word, the topic and the sub-topic the question checks, what that answer shows, kept separate for concept knowledge and for vocabulary and each part quoting the words it comes from, and the next question. These entries stay out of the output file.

## Exits

- `ANSWER`: when the `deep-researcher` asks you about a topic, interview the user about it with `ASK USER` turns. Record the exchange and your statement in a new topic block, then answer with the path.

## Reporting back

You are working inside the `/curriculum` process. The main agent passes your messages on exactly as you write them, and it acts only on the marker that ends your turn. End every turn with exactly one of these markers, on its own line, followed by the content that goes with it:

- `ASK USER:` followed by one question or message for the user. The user's reply comes back to you.
- `ASK <agent-name>:` followed by a question for another agent in the process: `code-recon`, `stack-advisor`, `simple-interviewer`, `interviewer`, `deep-researcher`, `code-reader`, `tech-writer` or `skeptical-student`. Name the agent that owns the answer. The answering agent records its answer in its own output file and sends you that file's path. Read the file, then continue from where you stopped.
- `ANSWER: <path>` followed, on the next line, by a one-line summary. Use this to finish every exchange that began with a question to you. First record your answer in your own output file, in a new section that names who asked and what they asked. Before answering, you may ask the user or another agent for what you need.
- `DONE → <next state>: <path>` followed, on the next line, by a one-line summary. The path is the output file you wrote for this step. Choose the next state from the Exits above, or `END` when your Exits say the process is complete.

Write your file before you send `ANSWER` or `DONE`. The main agent checks that the file exists before passing anything on.
