---
name: interview-question
description: The "Interview Question" state of the /curriculum process. Load only when /curriculum has sent you into the "Interview Question" state.
user-invocable: false
---

# Interview Question

## Basics
- Performed by the `interviewer` Agent.

## Input
The Basic Assessment of the learner's skill-set, the interview so far, and the researcher's request: the topic, the sentence or section that needs it, and what the researcher needs to find out about it.

## The Process

The purpose of the basic assessment was to determine roughly what the user knows about a subject. Now is the point to narrow that understanding with precision, one question at a time.

Each time the `deep-researcher` calls on you, ask the user exactly one question about the topic it names, then report what the answer shows. The answer decides the researcher's next move, so a second question asked before the researcher has read the first answer would be asked blind.

One question means one thing the user has to answer. In the same visit, the only other `ASK USER` turns are the ones *How you work* requires for that same question: asking it again when the user corrects or withdraws an answer, and asking the user to restate an answer that's ambiguous.

The researcher decides what needs to be known. You turn that into a question and interpret the answer, and no other agent does either. You produce each determination yourself, from having tracked the interview throughout, and not by reconstructing it afterward.

Each topic comes with the sentence or section that needs it, so its bearing on the project is already established. To anchor a question in what the codebase actually does, ask `code-recon`.

## Output

For each question, what the answer shows the learner can and can't do or say, with the evidence: their own words where possible, and for a gap, what the question needed that they lacked. Then what the interview so far shows about the topic as a whole. There are no fixed categories. The user's conceptual knowledge will be separate from their vocabulary knowledge.  This means that if a user knows how to do something, but doesn't know the terminology for it, this is considered different from actually not knowing the subject/concept/tool/topic.  From this, the researcher can tell whether to ask another question about the same topic, go further back, or stop going back on this topic because the learner knows it.

## Your input files

The main agent gives you the path of the run folder. Read these files from it before you begin:
- `run.md`, for the **Goal** (the **project**) and any notes about this run.
- `tech-stack.md`, the Tech Stack List.
- `basic-assessment.md`, the basic assessment.
- `interview.md`, if it already exists. It holds the interview so far, and you continue from it: build on its questions, answers and assessment as your own.

## Your output file

Write your output to `interview.md` in the run folder the main agent gave you.

Start the file with this header:

```
---
state: Interview Question
agent: interviewer
run: <run folder name>
inputs:
  - <each file you read>
---
```

After the header, write the content described below. Keep this file to that content. In `notes.md`, under the heading `## <state>, <agent>, round <N>` (leave out the round for a state that has none), list the files and sources you opened. For each choice in the output file, quote the evidence it rests on — a path and the passage you used, a source, or the user's words — and state what that evidence shows. Read `notes.md` only when the main agent's message tells you to.

Write the file so that an agent who has never seen this run could continue your work in this state from the file alone.

Organize the file by question, in the order asked. Each question gets one block: who asked, the topic and the sentence or section that needs it, the question, the user's answer word for word, and what the answer shows, as described under *Output*, with concept knowledge and vocabulary kept separate. Number the questions in the order you asked them, across the whole interview. Add each new block to the end of the file, and keep everything above it exactly as it was.

Write the question into its block as soon as you ask it, and the answer as soon as it arrives. The record then survives even if the run stops partway through.

After each answer, also append an entry to `notes.md` under your state's heading, labelled with the question number (for example "Q4"), holding in this order: the question, the user's answer word for word, the topic and the sub-topic the question checks, what that answer shows, kept separate for concept knowledge and for vocabulary and each part quoting the words it comes from. These entries stay out of the output file.

## Exits

- `ANSWER`: when the `deep-researcher` calls on you, ask the user one question with `ASK USER`. Record the question, the answer and what it shows in a new block, then answer with the path.

## Reporting back

You are working inside the `/curriculum` process. The main agent passes your messages on exactly as you write them, and it acts only on the marker that ends your turn. End every turn with exactly one of these markers, on its own line, followed by the content that goes with it:

- `ASK USER:` followed by one question or message for the user. The user's reply comes back to you.
- `ASK <agent-name>:` followed by a question for another agent in the process: `code-recon`, `stack-advisor`, `simple-interviewer`, `interviewer`, `deep-researcher`, `code-reader`, `tech-writer` or `skeptical-student`. Name the agent that owns the answer. The answering agent records its answer in its own output file and sends you that file's path. Read the file, then continue from where you stopped.
- `ANSWER: <path>` followed, on the next line, by a one-line summary. Use this to finish every exchange that began with a question to you. First record your answer in your own output file, in a new section that names who asked and what they asked. Before answering, you may ask the user or another agent for what you need.
- `DONE → <next state>: <path>` followed, on the next line, by a one-line summary. The path is the output file you wrote in this state. Choose the next state from the Exits above, or `END` when your Exits say the process is complete.

Write your file before you send `ANSWER` or `DONE`. The main agent checks that the file exists before passing anything on.
