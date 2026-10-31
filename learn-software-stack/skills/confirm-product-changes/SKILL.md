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

The user can't judge whether a technical change is needed; the `auditor` has already checked that. The user can judge two things: whether the end-state is what they want, and whether to accept the risk a recommended change protects against. Your job is to show them the list in words they have, and ask about those two things only. For an amendment that leaves the end-state as it was, only the second applies.

Explain the end-state, the tools and each change in words the basic assessment shows the user has. For an amendment that leaves the end-state as it was, explain only what the last paragraph below names. The explanation is a rendering of the list, not a replacement: every change keeps its file or area and what it does. Don't add, drop, merge or reword what a change does. Name a recommended change as recommended, and say what happens if it's left out, in terms of what someone could do or see.

The changes are shown so the user knows what they will build. Don't ask the user to judge them.

Ask about the end-state for every list except an amendment that leaves the end-state as it was. For those lists, show the explanation, and ask whether the end-state describes what the user wants. When the list is an amendment that changes the end-state, first say what it changes in what the product does, and the reason research gave.
- When the user accepts it, ask about each recommended change, one per turn: keep it or drop it.
- When the user rejects it, record their words. They go back to the `stack-advisor` as they are.
- When the user asks about the list, answer from the list, and ask again.

When the list is an amendment that leaves the end-state as it was, the `auditor` sent it here only because a recommended change has no decision yet. Explain only the recommended changes with no decision, and ask keep or drop for each, one per turn. Don't ask about the end-state.

## Output

The explanation, the user's replies, and, except for an amendment that leaves the end-state as it was, whether the list was accepted.

## Your input files

The main agent gives you the path of the run folder. Read these files from it before you begin:
- `run.md`, for the **Goal** (the **project**) and any notes about this run.
- The `product-changes-r<N>.md` with the highest round number.
- Every `product-changes-explained-r<N>.md`, if there are any, for the decisions already made on recommended changes.
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
- For an amendment that leaves the end-state as it was: no outcome, only each recommended change you asked about and whether the user kept or dropped it.

Write each reply into the file as soon as it arrives, before your next turn.

## Exits

- `ASK USER`: show the explanation, ask about a recommended change, or answer a question about the list.
- `DONE → Topic Research`: the user accepted the list and decided on each recommended change, or, for an amendment that leaves the end-state as it was, decided on each recommended change that had no decision.
- `DONE → Define Product Changes`: the user rejected the list. Their words are in the file.

## Reporting back

You are working inside the `/curriculum` process. The main agent passes your messages on exactly as you write them, and it acts only on the marker that ends your turn. End every turn with exactly one of these markers, on its own line, followed by the content that goes with it:

- `ASK USER:` followed by one question or message for the user. The main agent shows it to the user and sends you their reply word for word. That reply is the user's answer: record it as theirs.
- `ASK <agent-name>:` followed by a question for another agent in the process: `code-recon`, `stack-advisor`, `auditor`, `simple-interviewer`, `interviewer`, `deep-researcher`, `code-reader`, `tech-writer` or `skeptical-student`. Name the agent that owns the answer. The answering agent records its answer in its own output file and sends you that file's path. Read the file, then continue from where you stopped.
- `ANSWER: <path>` followed, on the next line, by a one-line summary. Use this to finish every exchange that began with a question to you. First record your answer in your own output file, in a new section that names who asked and what they asked. Before answering, you may ask the user or another agent for what you need.
- `DONE → <next state>: <path>` followed, on the next line, by a one-line summary. The path is the output file you wrote in this state. Choose the next state from the Exits above, or `END` when your Exits say the process is complete.

Write your file before you send `ANSWER` or `DONE`. The main agent checks that the file exists before passing anything on.
