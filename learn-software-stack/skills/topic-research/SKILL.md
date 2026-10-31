---
name: topic-research
description: The "Topic Research" state of the /curriculum process. Load only when /curriculum has sent you into the "Topic Research" state.
user-invocable: false
---

# Topic Research

## Basics
- Performed by the `deep-researcher` Agent.

## Input
The accepted changes, the Basic Assessment, which is what the learner says they know of each tool and concept the changes involve, and the interview record, if one exists. The interview record grows as you ask the interviewer about topics.

## The Process
Now the task is the research to establish the curriculum of documentation that the user would need to get from their current state of knowledge to the state of knowledge necessary to make each accepted change. Start from each change's Involves line.  The following are some of the places the researcher could go in order to find documentation.

- Reading the online documentation on the component from the official website. 
- Reading the Forums or articles on the component. 

The research is recursive, and what the learner knows decides where it stops. For example, in order to know Postgres, you need to know SQL. Work one topic at a time, starting from what each accepted change needs directly and working backward:

1. Find the section that explains the topic, and list its prerequisites: the terms in its text, the terms inside each defining sentence you intend to quote, and the concepts it builds on. A prerequisite can be as small as one definition or as large as a section to read.
2. Test each prerequisite against the evidence so far: the basic assessment, the interview record, and the entries you have already written. Then do exactly one of the following:

   1. **The evidence shows the learner knows it.** Stop there. Record what shows it. A claim in the basic assessment is not enough on its own; only the interview record or an entry you have already written can show it.
   2. **The evidence is silent, or shows a gap, and an accepted change needs it.** When the basic assessment shows the learner has never met it, skip the interview: find the source that explains the topic, and test that source's prerequisites the same way. Otherwise `ASK interviewer` about it. Name the topic, and quote the sentence or section that needs it. When the interviewer reports a gap, find the source that explains the topic, and test that source's prerequisites the same way.
   3. **No accepted change needs it.** Record it as not pertinent, with the reason, and list it under the entry's **Ignorable**. Do not ask about it.

Each `ASK interviewer` names one topic and gets back one answered question. Read what the answer shows before your next move: ask another question about the same topic, go back to its source and that source's prerequisites, or stop going back on this topic because the learner knows it (case 1). Write each curriculum entry when every prerequisite of its section has ended; don't draft the curriculum ahead of the interview. Test: each `ASK interviewer` names one topic, and each one after the first was sent after you read the answer to the one before it.

Test: for every topic you send the interviewer, you can quote the sentence or section that needs it, and name the accepted change that section serves. A prerequisite you can't link that way is case 3. `[judgment]`

You do not judge what the learner knows. You read the interviewer's determination, which says specifically what they can and can't do, and decide from it whether to ask another question about the same topic, go further back, or stop going back on it. Research is finished when no topic is left open: every topic the accepted changes need, and every prerequisite you found along the way, has ended in case 1 or case 3, or is defined by a sentence whose own prerequisites all ended in case 1.

Every question to the interviewer goes to the same `interviewer` instance, so that it folds each answer into one coherent determination of the learner.

Research adds what the learner must learn, never what the product does. A knowledge gap can add a prerequisite entry; it can't add a change. When an accepted change can't be made as written, or needs a change the list doesn't have, take the `DONE → Define Product Changes` exit below.

When you resume after an amendment, update the subject list of each change the amendment changed or added, write the entries those lists need, and remove every entry that only a removed change needed.

## Output
The list of Documentation that is necessary to get the user from their current state to the state in which they know enough to make the accepted changes. This will be referred to as the curriculum. The curriculum shall be in an order in which the human user is expected to read the material. This means that no subject shall contain material that has not been learned in a previous subject.

For each accepted change, its subject list: every subject the learner must learn to make it, prerequisites included. The curriculum is the union of those lists, each subject once, in reading order. Each entry names every accepted change it serves, and shall carry three lists:

1. **Terms:** each term the learner needs from the entry's section that no earlier entry defines. A term is needed when the interview assessment shows the user does not use it correctly, or when the section uses it and cannot be followed without it. Each term is listed with the defining sentence quoted verbatim from its source, and the source and section it comes from. The definition comes from the documentation of the language or tool the term belongs to, and lets the learner understand how the change that needs it uses the term. Quote exactly one, whole and word for word. When no source defines the term, the entry says "no source defines this" and does not supply a definition of its own.
2. **Ignorable:** what in the assigned section the learner does not need, such as terms or subsections, so the writer can list each as a `Skip:` bullet.
3. **Trace:** for each prerequisite you tested while writing the entry, where the check stopped and why: the learner knows it (the evidence), a quoted sentence defines it and the learner knows every prerequisite of that sentence (the sentence), or no accepted change needs it (the reason).

## Your input files

The main agent gives you the path of the run folder. Read these files from it before you begin:
- `run.md`, for the **Goal** (the **project**) and any notes about this run.
- The `product-changes-r<N>.md` with the highest round number, which is the accepted list, and every `product-changes-explained-r<N>.md`. For each recommended change, the most recent explanation that records a decision on it decides whether it is kept.
- `basic-assessment.md`, the basic assessment.
- `interview.md`, the interview record, if it exists.
- Every `code-review-*.md` file in the folder, if there are any. Code review is optional, and most runs have none.
- `curriculum.md`, if it already exists. It holds your research so far, and you continue from it.

## Your output file

Write your output to `curriculum.md` in the run folder the main agent gave you.

Start the file with this header:

```
---
state: Topic Research
agent: deep-researcher
run: <run folder name>
inputs:
  - <each file you read>
---
```

After the header, write the content described below. Keep this file to that content. In `notes.md`, under the heading `## <state>, <agent>, round <N>` (leave out the round for a state that has none), list the files and sources you opened. For each choice in the output file, quote the evidence it rests on — a path and the passage you used, a source, or the user's words — and state what that evidence shows. Read `notes.md` only when the main agent's message tells you to.

Write the file so that an agent who has never seen this run could continue your work in this state from the file alone.

The file contains:
- The curriculum described under *Output*, in reading order.
- Each accepted change's subject list, naming its curriculum entries.
- The sources you opened for each subject/concept/topic/tool, and for each one whether the curriculum includes it or leaves it out.
- One section for each question another agent asked you, naming who asked and what you found.
- One section for each finding that sent an accepted change back to *Define Product Changes*: which change, what shows it, and why it can't be made as written.

## Exits

- `DONE → Write the Lesson Plan`: no topic is left open, as described under *The Process*.
- `DONE → Define Product Changes`: an accepted change can't be made as written, or needs a change the list doesn't have. Record which change, what shows it, and why, in `curriculum.md` first.
- `ASK interviewer` (round trip, "Learner's Knowledge Unknown"): the evidence does not show whether the learner knows a topic an accepted change needs. Name one topic, quote what needs it, name the change it serves, and say what you need to find out about it. The interviewer records the exchange in the interview file and sends you its path, and you continue your research.
- `ASK code-reader` (round trip, "Something's wrong with Doc"): the documentation disagrees with itself or with how the subject/concept/topic/tool actually behaves. Name the repository (with a URL), the version or branch, and the exact claim to check. The code-reader sends you the path of its findings file, and you continue your research.
- `ANSWER`: when another agent asks you for more information, research it, record what you found in your output file, and answer with its path.

## Reporting back

You are working inside the `/curriculum` process. The main agent passes your messages on exactly as you write them, and it acts only on the marker that ends your turn. End every turn with exactly one of these markers, on its own line, followed by the content that goes with it:

- `ASK USER:` followed by one question or message for the user. The main agent shows it to the user and sends you their reply word for word. That reply is the user's answer: record it as theirs.
- `ASK <agent-name>:` followed by a question for another agent in the process: `code-recon`, `stack-advisor`, `auditor`, `simple-interviewer`, `interviewer`, `deep-researcher`, `code-reader`, `tech-writer` or `skeptical-student`. Name the agent that owns the answer. The answering agent records its answer in its own output file and sends you that file's path. Read the file, then continue from where you stopped.
- `ANSWER: <path>` followed, on the next line, by a one-line summary. Use this to finish every exchange that began with a question to you. First record your answer in your own output file, in a new section that names who asked and what they asked. Before answering, you may ask the user or another agent for what you need.
- `DONE → <next state>: <path>` followed, on the next line, by a one-line summary. The path is the output file you wrote in this state. Choose the next state from the Exits above, or `END` when your Exits say the process is complete.

Write your file before you send `ANSWER` or `DONE`. The main agent checks that the file exists before passing anything on.
