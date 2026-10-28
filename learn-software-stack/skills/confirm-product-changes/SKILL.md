---
name: confirm-product-changes
description: The "Confirm Product Changes" state of the /curriculum process, run by simple-interviewer. Load only when /curriculum has sent you into the "Confirm Product Changes" state.
user-invocable: false
---

# Confirm Product Changes

## Basics

- Performed by the `simple-interviewer` Agent.

## Input

- The change list: the end-state, the tools, and the changes.
- The basic assessment, for the words the user has.

## The Process

The user can't write the change list, but they can tell whether it describes what they want. Your job is to show them the list in words they have, and find out.

Explain the end-state, the tools and each change in words the basic assessment shows the user has. The explanation is a rendering of the list, not a replacement: every change keeps its file or area and what it does. Don't add, drop, merge or reword what a change does. Name a recommended change as recommended, and say what it protects against.

When the list is an amendment, say what it changes and the reason research gave, before asking whether it describes what the user wants.

Show the explanation, and ask whether it describes what the user wants.
- When the user accepts it, ask about each recommended change, one per turn: keep it or drop it.
- When the user rejects it, record their words. They go back to the `stack-advisor` as they are.
- When the user asks about the list, answer from the list, and ask again.

## Output

The explanation, the user's replies, and whether the list was accepted.

## Your input files

The main agent gives you the path of the run folder. Read these files from it before you begin:
- `run.md`, for the **Goal** (the **project**) and any notes about this run.
- The `product-changes-r<N>.md` with the highest round number.
- `basic-assessment.md`, the basic assessment.

## Your output file

Write your output to `product-changes-explained-r<N>.md` in the run folder the main agent gave you, with the same `<N>` as the list it explains.

Start the file with this header:

```
---
state: Confirm Product Changes
agent: simple-interviewer
run: <run folder name>
inputs:
  - <each file you read>
---
```

After the header, write the content described below. Keep this file to that content. In `notes.md`, under the heading `## <state>, <agent>, round <N>` (leave out the round for a state that has none), list the files and sources you opened. For each choice in the output file, quote the evidence it rests on — a path and the passage you used, a source, or the user's words — and state what that evidence shows. Read `notes.md` only when the main agent's message tells you to.

Write the file so that an agent who has never seen this run could continue your work in this state from the file alone.

The file contains:
- The explanation, exactly as you showed it.
- Each of the user's replies, word for word.
- **Outcome:** accepted or rejected.
- When accepted: each recommended change, and whether the user kept or dropped it.

Write each reply into the file as soon as it arrives, before your next turn.

## Exits

- `ASK USER`: show the explanation, ask about a recommended change, or answer a question about the list.
- `DONE → Topic Research`: the user accepted the list and decided on each recommended change.
- `DONE → Define Product Changes`: the user rejected the list. Their words are in the file.

## Reporting back

You are working inside the `/curriculum` process. The main agent passes your messages on exactly as you write them, and it acts only on the marker that ends your turn. End every turn with exactly one of these markers, on its own line, followed by the content that goes with it:

- `ASK USER:` followed by one question or message for the user. The main agent shows it to the user and sends you their reply word for word. That reply is the user's answer: record it as theirs.
- `ASK <agent-name>:` followed by a question for another agent in the process: `code-recon`, `stack-advisor`, `simple-interviewer`, `interviewer`, `deep-researcher`, `code-reader`, `tech-writer` or `skeptical-student`. Name the agent that owns the answer. The answering agent records its answer in its own output file and sends you that file's path. Read the file, then continue from where you stopped.
- `ANSWER: <path>` followed, on the next line, by a one-line summary. Use this to finish every exchange that began with a question to you. First record your answer in your own output file, in a new section that names who asked and what they asked. Before answering, you may ask the user or another agent for what you need.
- `DONE → <next state>: <path>` followed, on the next line, by a one-line summary. The path is the output file you wrote in this state. Choose the next state from the Exits above, or `END` when your Exits say the process is complete.

Write your file before you send `ANSWER` or `DONE`. The main agent checks that the file exists before passing anything on.
