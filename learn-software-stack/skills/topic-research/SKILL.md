---
name: topic-research
description: Step 4 of the /curriculum process ("Topic Research"). Load only when /curriculum has sent you into the "Topic Research" state.
user-invocable: false
---

# Topic Research

## Basics
- Performed by the `deep-researcher` Agent.

## Input
The Interview results with each subject/concept/topic/tool, and the user's knowledge of it. 

## The Process
Now the task is the research on each subject/concept/topic/tool to establish the curriculum of documentation that the user would need to get from their current state of knowledge, to the state of knowledge necessary to complete the work for the project.  The following are some of the place that the researcher could go in order to 

- Reading the online documentation on the component from the official website. 
- Reading the Forums or articles on the component. 

The research process will likely be recursive. eg: in order to know Postgres, you need to know SQL.  So the research can stop once it crosses into the knowledge base of the user.

It may be possible that the *Topic Research* process discovers further prerequisites to a given subject/concept/topic/tool.  This could be either a situation where a new prerequisite subject/concept/topic/tool is discovered, or there is simply more information about the subject/concept/topic/tool that wasn't assessed relative to the user's knowledge. In either case, it may be necessary to go back to the *User Interview* and ask more questions to the user. This loop-back shall resume the same `interviewer` agent instance used for the original interview, not spawn a new one — the agent needs the full history of prior answers to fold the new question into one coherent determination, rather than producing a second, disconnected assessment.

Another agent may ask you whether a topic can be practiced in the project, and where. Answer from the Tech Stack List and your research. When that isn't enough, `ASK code-reader` for the real location, and report what it found.

## Output
The list of Documentation that is necessary to get the user from their current state to the state in which they know enough to complete the task for the project. This will be referred to as the curriculum. The curriculum shall be in an order in which the human user is expected to read the material. This means that no subject shall contain material that has not been learned in a previous subject.

Each entry in the curriculum shall carry two lists:

1. **Terms:** each term the learner needs from the entry's section that no earlier entry defines. A term is needed when the interview assessment shows the user does not use it correctly, or when the section uses it and cannot be followed without it. Each term is listed with the defining sentence quoted verbatim from its source, and the source and section it comes from. When no source defines the term, the entry says "no source defines this" and does not supply a definition of its own.
2. **Ignorable:** what in the assigned section the learner does not need, such as terms or subsections, so the writer can mark each as safe to ignore.

## Your input files

The main agent gives you the path of the run folder. Read these files from it before you begin:
- `run.md`, for the **Goal** (the **project**) and any notes about this run.
- `01-tech-stack.md`, the Tech Stack List.
- `02-basic-assessment.md`, the basic assessment.
- `03-interview.md`, the interview record, including any Follow-up sections.
- Every `05-code-review-*.md` file in the folder, if there are any. Code review is optional, and most runs have none.
- `04-curriculum.md`, if it already exists. It holds your research so far, and you continue from it.

## Your output file

Write your output to `04-curriculum.md` in the run folder the main agent gave you.

Start the file with this header:

```
---
step: Topic Research
agent: deep-researcher
run: <run folder name>
inputs:
  - <each file you read>
---
```

After the header, write the content described below. Keep this file to that content. In `notes.md`, under the heading `## <step>, <agent>, round <N>` (leave out the round for a step that has none), list the files and sources you opened. For each choice in the output file, quote the evidence it rests on — a path and the passage you used, a source, or the user's words — and state what that evidence shows. Read `notes.md` only when the main agent's message tells you to.

Write the file so that an agent who has never seen this run could continue your step from the file alone.

The file contains:
- The curriculum described under *Output*, in reading order.
- The sources you opened for each subject/concept/topic/tool, and for each one whether the curriculum includes it or leaves it out.
- One section for each question another agent asked you, naming who asked and what you found.

## Exits

- `DONE → Write the Lesson Plan`: the research is compiled into the curriculum.
- `ASK interviewer` (round trip, "Sub-Topic Discovered"): you found a prerequisite, or more about a subject/concept/topic/tool, that the interview did not assess. Name the sub-topic. The interviewer records the follow-up in the interview file and sends you its path, and you continue your research.
- `ASK code-reader` (round trip, "Something's wrong with Doc"): the documentation disagrees with itself or with how the subject/concept/topic/tool actually behaves. Name the repository (with a URL), the version or branch, and the exact claim to check. The code-reader sends you the path of its findings file, and you continue your research.
- `ANSWER`: when another agent asks you for more information, research it, record what you found in your output file, and answer with its path.

## Reporting back

You are working inside the `/curriculum` process. The main agent passes your messages on exactly as you write them, and it acts only on the marker that ends your turn. End every turn with exactly one of these markers, on its own line, followed by the content that goes with it:

- `ASK USER:` followed by one question or message for the user. The user's reply comes back to you.
- `ASK <agent-name>:` followed by a question for another agent in the process: `code-recon`, `stack-advisor`, `simple-interviewer`, `interviewer`, `deep-researcher`, `code-reader`, `tech-writer` or `skeptical-student`. Name the agent that owns the answer. The answering agent records its answer in its own output file and sends you that file's path. Read the file, then continue from where you stopped.
- `ANSWER: <path>` followed, on the next line, by a one-line summary. Use this to finish every exchange that began with a question to you. First record your answer in your own output file, in a new section that names who asked and what they asked. Before answering, you may ask the user or another agent for what you need.
- `DONE → <next state>: <path>` followed, on the next line, by a one-line summary. The path is the output file you wrote for this step. Choose the next state from the Exits above, or `END` when your Exits say the process is complete.

Write your file before you send `ANSWER` or `DONE`. The main agent checks that the file exists before passing anything on.
