---
name: topic-code-review
description: Step 5 of the /curriculum process ("Topic Code Review"). Load only when /curriculum has sent you into the "Topic Code Review" state.
user-invocable: false
---

# Topic Code Review

The *Topic Research* may find what the documentation says simply does not align with the actual functionality of the subject/concept/topic/tool, or that there are different docs out there that don't agree. In this case, we must look at the source code for whatever subject/concept/topic/tool is in question to determine the truth. If there's something we don't know about SQLAlchemy, for instance, maybe we have to look at the source for it.  This should be expected to be a very rare occurrence. 

This state is not limited to resolving items Topic Research explicitly flagged as uncertain. It must also spot-check any code claim baked into the User Interview questions or Topic Research findings against the actual source, regardless of whether anyone flagged it — a confidently stated claim is not evidence it was verified. This applies with equal weight to claims embedded in an applied portion — a file path, a command, a predicted output, or a described failure mode is exactly the kind of claim this state exists to verify, and getting one wrong is worse here than in a reading list, since the user acts on it directly.

## Your input files

The main agent gives you the path of the run folder. Read these files from it before you begin:
- `run.md`, for the **Goal** (the **project**) and any notes about this run.
- The question from `deep-researcher`, which the main agent passes to you. It names the claim to check.
- The source the main agent prepared for you as plain files. The main agent tells you where it is.

## Your output file

Write your output to `05-code-review-<topic>.md` in the run folder the main agent gave you. Replace `<topic>` with a short, lowercase, hyphenated name for the claim you checked. If that file already exists, add `-2`, `-3` and so on.

Start the file with this header:

```
---
step: Topic Code Review
agent: code-reader
run: <run folder name>
inputs:
  - <each file you read>
---
```

After the header, write the content described below. Keep this file to that content. In `notes.md`, under the heading `## <step>, <agent>, round <N>` (leave out the round for a step that has none), list the files and sources you opened. For each choice in the output file, quote the evidence it rests on — a path and the passage you used, a source, or the user's words — and state what that evidence shows. Read `notes.md` only when the main agent's message tells you to.

Write the file so that an agent who has never seen this run could continue your step from the file alone.

The file contains:
- The claim you checked, word for word.
- The source you read: the repository, the version or branch, and the files.
- Your findings.

## Exits

- `ANSWER`: this state is always a round trip. `deep-researcher` asks you to check a claim. Write your findings file, then answer with its path.

## Reporting back

You are working inside the `/curriculum` process. The main agent passes your messages on exactly as you write them, and it acts only on the marker that ends your turn. End every turn with exactly one of these markers, on its own line, followed by the content that goes with it:

- `ASK USER:` followed by one question or message for the user. The user's reply comes back to you.
- `ASK <agent-name>:` followed by a question for another agent in the process: `code-recon`, `stack-advisor`, `simple-interviewer`, `interviewer`, `deep-researcher`, `code-reader`, `tech-writer` or `skeptical-student`. Name the agent that owns the answer. The answering agent records its answer in its own output file and sends you that file's path. Read the file, then continue from where you stopped.
- `ANSWER: <path>` followed, on the next line, by a one-line summary. Use this to finish every exchange that began with a question to you. First record your answer in your own output file, in a new section that names who asked and what they asked. Before answering, you may ask the user or another agent for what you need.
- `DONE → <next state>: <path>` followed, on the next line, by a one-line summary. The path is the output file you wrote for this step. Choose the next state from the Exits above, or `END` when your Exits say the process is complete.

Write your file before you send `ANSWER` or `DONE`. The main agent checks that the file exists before passing anything on.
