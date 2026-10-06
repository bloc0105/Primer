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

## Output
The list of Documentation that is necessary to get the user from their current state to the state in which they know enough to complete the task for the project. This will be referred to as the curriculum. The curriculum shall be in an order in which the human user is expected to read the material. This means that no subject shall contain material that has not been learned in a previous subject.

## Your input files

The main agent gives you the path of the run folder. Read these files from it before you begin:
- `run.md`, for the user's request (the **project**) and any notes about this run.
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

After the header, write the content described below. Do not put your reasoning in this file. Append it to `notes.md` in the run folder, under the heading `## <step>, <agent>, round <N>` (leave out the round for a step that has none), covering what you looked at, what you weighed, and why you decided as you did. Read `notes.md` only when the main agent's message tells you to.

Write the file so that an agent who has never seen this run could continue your step from the file alone.

The file contains:
- The curriculum described under *Output*, in reading order.
- The sources you considered for each subject/concept/topic/tool, and why you chose or dropped each one.
- One section for each question another agent asked you, naming who asked and what you found.

## Exits

- `DONE → Write the Lesson Plan`: the research is compiled into the curriculum.
- `ASK interviewer` (round trip, "Sub-Topic Discovered"): you found a prerequisite, or more about a subject/concept/topic/tool, that the interview did not assess. Name the sub-topic. The interviewer records the follow-up in `03-interview.md` and sends you the path, and you continue your research.
- `ASK code-reader` (round trip, "Something's wrong with Doc"): the documentation disagrees with itself or with how the subject/concept/topic/tool actually behaves. Name the repository (with a URL), the version or branch, and the exact claim to check. The code-reader sends you the path of its findings file, and you continue your research.
- `ANSWER`: when `tech-writer` asks you for more information, research it, record what you found in `04-curriculum.md`, and answer with the path.

## Reporting back

You are working inside the `/curriculum` process. The main agent passes your messages on exactly as you write them, and it acts only on the marker that ends your turn. End every turn with exactly one of these markers, on its own line, followed by the content that goes with it:

- `ASK USER:` followed by one question or message for the user. The user's reply comes back to you.
- `ASK <agent-name>:` followed by a question for another agent in the process: `code-recon`, `stack-advisor`, `simple-interviewer`, `interviewer`, `deep-researcher`, `code-reader`, `tech-writer` or `skeptical-student`. Name the agent that owns the answer. The answering agent records its answer in its own output file and sends you that file's path. Read the file, then continue from where you stopped.
- `ANSWER: <path>` followed, on the next line, by a one-line summary. Use this to finish every exchange that began with a question to you. First record your answer in your own output file, in a new section that names who asked and what they asked. Before answering, you may ask the user or another agent for what you need.
- `DONE → <next state>: <path>` followed, on the next line, by a one-line summary. The path is the output file you wrote for this step. Choose the next state from the Exits above, or `END` when your Exits say the process is complete.

Write your file before you send `ANSWER` or `DONE`. The main agent checks that the file exists before passing anything on.
