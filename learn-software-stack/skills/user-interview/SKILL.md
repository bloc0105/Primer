---
name: user-interview
description: Step 3 of the /curriculum process ("User Interview"). Load only when /curriculum has sent you into the "User Interview" state.
user-invocable: false
---

# User Interview

## Basics
- Performed by the `interviewer` Agent.

## Input
The Basic Assessment of the learner's skill-set.

## The Process

The purpose of the basic assessment was to determine roughly what the user knows about a subject. Now is the point to narrow that understanding with precision.

At this point, the user is interviewed to determine their knowledge of the various subjects/concepts/topics/tools. The interview shall be invoked iteratively: one question per call, with the main agent relaying that question to the user, then relaying the user's answer back to that same agent instance before requesting the next question. 

Since the basic assessment already covered some topics, the interview should account for this, which will expedite the interviewer process.  For instance, if the user explicitly said they know nothing about a certain subject/concept/topic/tool, it's probably not necessary to ask them about it.  

The main agent does not choose what to ask, interpret an answer, or decide when the interview ends — that authority belongs to the `interviewer` agent alone, which also produces the final determination itself, from having tracked the interview throughout, rather than the AI reconstructing it afterward.

The `interviewer` may, however, need to establish relevance of its questions to the project itself, and should be asking the main agent, who may forward questions to other agents, whether it's question has pertinence, so as to not ask questions that have no bearing on the project. 

## Output

This will be the same list as the list that was established by the basic assessment, but with significantly more precision, describing exactly which sub-topics of a subject/concept/topic/tool the user is familiar with, and where the gaps lie. The user's conceptual knowledge will be separate from their vocabulary knowldge.  This means that if a user knows how to do something, but doesn't know the terminology for it, this is considered different from actually not knowing the subject/concept/tool/topic.  From this, the interview can tell exactly what things the user must learn in orer to complete the work necessary to accomplish the objectives of the project.

## Your input files

The main agent gives you the path of the run folder. Read these files from it before you begin:
- `run.md`, for the user's request (the **project**) and any notes about this run.
- `01-tech-stack.md`, the Tech Stack List.
- `02-basic-assessment.md`, the basic assessment.
- `03-interview.md`, if it already exists. It holds the interview so far, and you continue from it: build on its questions, answers and assessment as your own.

## Your output file

Write your output to `03-interview.md` in the run folder the main agent gave you. Add each question and the user's answer to the file as soon as the answer arrives, before you ask the next question, so the record survives even if the run stops partway through.

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

After the header, write the content described below. End the file with a `## How I got here` section that explains how you reached your conclusions: what you looked at, what you weighed, and why you decided as you did.

Write the file so that an agent who has never seen this run could continue your step from the file alone.

The file contains:
- Every question you asked, and the user's answer, word for word, in order.
- The final assessment described under *Output*, with concept knowledge and vocabulary kept separate.
- One **Follow-up** section for each follow-up interview. Each one names the agent that asked and why, and holds its own questions, answers and updated determination. Add follow-ups to the end of the file, and keep everything above them exactly as it was.

## Exits

- `DONE → Topic Research`: the interview is complete and the user is assessed.
- `ANSWER`: when another agent asks you about a sub-topic, for example `deep-researcher` after finding a new prerequisite, interview the user about it with `ASK USER` turns. Record the exchange and your updated determination in a new Follow-up section, then answer with the path.

## Reporting back

You are working inside the `/curriculum` process. The main agent passes your messages on exactly as you write them, and it acts only on the marker that ends your turn. End every turn with exactly one of these markers, on its own line, followed by the content that goes with it:

- `ASK USER:` followed by one question or message for the user. The user's reply comes back to you.
- `ASK <agent-name>:` followed by a question for another agent in the process: `code-recon`, `stack-advisor`, `simple-interviewer`, `interviewer`, `deep-researcher`, `code-reader`, `tech-writer` or `skeptical-student`. Name the agent that owns the answer. The answering agent records its answer in its own output file and sends you that file's path. Read the file, then continue from where you stopped.
- `ANSWER: <path>` followed, on the next line, by a one-line summary. Use this to finish every exchange that began with a question to you. First record your answer in your own output file, in a new section that names who asked and what they asked. Before answering, you may ask the user or another agent for what you need.
- `DONE → <next state>: <path>` followed, on the next line, by a one-line summary. The path is the output file you wrote for this step. Choose the next state from the Exits above, or `END` when your Exits say the process is complete.

Write your file before you send `ANSWER` or `DONE`. The main agent checks that the file exists before passing anything on.
