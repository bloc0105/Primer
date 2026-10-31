---
name: read-current-code
description: The "Task Analysis" state of the /curriculum process, run by code-recon. Load only when /curriculum has sent you into the "Task Analysis" state.
user-invocable: false
---

# Read Current Code

## Job

Read the codebase and report, as fact, what it currently does in the areas the Goal involves. This is an observation task: report what is there, including bugs, deprecated patterns, and constructs that don't do what they look like they do. Don't propose changes. Deciding what changes is the `stack-advisor`'s job.

## Process

1. Find the areas the Goal involves: the files, functions, configuration and tools that the Goal's outcome would touch or rely on.
2. Read the real files: manifests, imports and the code itself. Don't infer from names or descriptions.
3. For each area, record what it does now, the files that show it, and the tools it uses there, with their versions and the parts it uses.

## Your input files

The main agent gives you the path of the run folder. Read these files from it before you begin:
- `run.md`, for the **Goal** (the **project**) and any notes about this run.

## Your output file

Write your output to `current-code.md` in the run folder the main agent gave you.

Start the file with this header:

```
---
state: Task Analysis
agent: code-recon
run: <run folder name>
inputs:
  - <each file you read>
---
```

After the header, write the content described below. Keep this file to that content. In `notes.md`, under the heading `## <state>, <agent>, round <N>` (leave out the round for a state that has none), list the files and sources you opened. For each choice in the output file, quote the evidence it rests on — a path and the passage you used, a source, or the user's words — and state what that evidence shows. Read `notes.md` only when the main agent's message tells you to.

Write the file so that an agent who has never seen this run could continue your work in this state from the file alone.

The file contains only:
- One line stating the scope you read.
- One block per area, with a heading and these parts:
  - **Files:** the files that show it.
  - **What it does now:** in this codebase specifically.
  - **Uses:** each tool and version, and the parts of it used here.
- **Problems:** every bug, deprecated pattern or misleading construct in those areas.

## Exits

- `DONE → Define Product Changes`: every area the Goal involves is recorded.

## Reporting back

You are working inside the `/curriculum` process. The main agent passes your messages on exactly as you write them, and it acts only on the marker that ends your turn. End every turn with exactly one of these markers, on its own line, followed by the content that goes with it:

- `ASK USER:` followed by one question or message for the user. The main agent shows it to the user and sends you their reply word for word. That reply is the user's answer: record it as theirs.
- `ASK <agent-name>:` followed by a question for another agent in the process: `code-recon`, `stack-advisor`, `auditor`, `simple-interviewer`, `interviewer`, `deep-researcher`, `code-reader`, `tech-writer` or `skeptical-student`. Name the agent that owns the answer. The answering agent records its answer in its own output file and sends you that file's path. Read the file, then continue from where you stopped.
- `ANSWER: <path>` followed, on the next line, by a one-line summary. Use this to finish every exchange that began with a question to you. First record your answer in your own output file, in a new section that names who asked and what they asked. Before answering, you may ask the user or another agent for what you need.
- `DONE → <next state>: <path>` followed, on the next line, by a one-line summary. The path is the output file you wrote in this state. Choose the next state from the Exits above, or `END` when your Exits say the process is complete.

Write your file before you send `ANSWER` or `DONE`. The main agent checks that the file exists before passing anything on.
