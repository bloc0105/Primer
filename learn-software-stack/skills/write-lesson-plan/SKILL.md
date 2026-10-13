---
name: write-lesson-plan
description: Step 6 of the /curriculum process ("Write the Lesson Plan"). Load only when /curriculum has sent you into the "Write the Lesson Plan" state.
user-invocable: false
---

# Write the Lesson Plan

## Basics

- Performed by the `tech-writer` Agent.

## Input

- The curriculum from the Research State.
- The interview assessmentof the user.

## The Process

This is where the lesson plan is actually created.  Everything from the curriculum must have a practical application to the project. 

The lesson plan shall be a list of citations to documentation, plus a practical for each unit. The documentation teaches, and the plan says what to read. Each of these shall be true of the plan file, and each can be checked by searching it:

1. It does not mention the interview, a review, a revision round, or how the plan was made.
2. It does not contain "you" or "your", outside quotations.
3. Every item in a Vocabulary or Reading sub-section is one citation.
4. Each citation carries at most one sentence of the plan's own words, which says what the learner gets from it.
5. No Vocabulary or Reading sub-section contains a code block, definition or analogy that the plan wrote. A definition is quoted verbatim from its source, with a link.

**One exception.** When the cited documentation is wrong for this project, or does not explain something the learner needs, a citation may carry a note of up to two sentences. The note says what is wrong or missing and what is true instead, and names the section it corrects. Your `notes.md` entry lists each note with the reason.

Each unit of the lesson shall contain three sub-sections, in this order:

1. **Vocabulary:** each term that the unit's readings use, that the learner needs, and that the interview assessment does not show the user already using correctly. Each entry is the term, the defining sentence quoted from its source, and a link to that source. A term appears in the unit where it is first needed and nowhere else. When no source defines a term, `ASK deep-researcher` for one before writing a correction note. A unit that needs no terms says so.
2. **Reading:** the documentation that the user needs to read in order to be effective with that subject. If only a specific section of a page is what the user doesn't already know, assign that section and not the whole page, and say which one.
3. **Practical:** a practical application of the lesson in the project itself.  This will tell the user where the work is and what to fix or add, and not much more. The work should be pertinent to that section of the lesson.

Each reading item shall satisfy every rule below, and each is a yes/no test:

1. It names the parent section first, links to it, and then lists the subsections to read, such as "go to section X.1, read X.1.2, X.1.4 and X.1.5", with the link on the parent section.
2. It names what to read by section number or heading, and does not describe how the page looks (a box, a sidebar, a table).
3. It lists anything in the assigned sections that the learner does not need and that no Vocabulary entry defines, marked at the point where it appears as safe to ignore, such as "metaclasses appear here and can be ignored".

The plan shall begin with Unit 0, whose practical is running the project as it stands and observing how it behaves, so that later results can be compared with it. Unit 0 includes the setup needed to run the project only when the interview assessment shows the user cannot run it already. Its Vocabulary and Reading sub-sections are whatever the user needs to run the project at all, and either may say that none is needed. Its outcome is that the project runs, so rule 2 below does not apply to it.

Each practical step shall satisfy every rule below, and each is a yes/no test:

1. It names the file or area of the project where the work happens.
2. It states a change to make there as a result (fix this, add that), and leaves the method to the learner.
3. It states a result the learner can observe, and how to observe it: a command's output, a test passing, or how the running project behaves.
4. Its completion never depends on a written output: a note, list, explanation, prediction or decision.
5. It creates no scratch file, folder, or throwaway edit. Running the project, its tests, or a tool is fine when it serves the change.
6. It uses only concepts taught earlier in the plan, with one exception: it may use code from a later unit when the step says so by name where the code appears, such as "write this code, don't worry about what it means yet, it is covered in Unit 6; the point here is X".

One more check cannot be made yes/no, so it is a stated judgment: the change should move the project toward the Goal. In your `notes.md` entry, record for each practical which part of the Goal it advances.

When a topic in the curriculum has no project change to practice, ask whether it belongs and where it can be practiced. Never drop it silently, and never invent a practical for it.

## Other Considerations

- Exercises should default toward open-ended framing. Rather than handing the learner a fully-specified function signature and skeleton body, prefer pointing at a real file and a real-world scenario and letting them work out the shape — e.g. "apply what you learned about `except ... as e` to `main.py`".
- Tune each unit to the user's knowledge by what it assigns, lists and skips: which terms, which sections, where to stop, what to ignore. Never by writing explanation, and never by addressing the reader or retelling what they said.
- The `tech-writer` may have questions during writing.  It is up to the main agent to decide which agent to pass the questions to.

## Output
The completed lesson plan for the user

## Your input files

The main agent gives you the path of the run folder. Read these files from it before you begin:
- `run.md`, for the **Goal** (the **project**) and any notes about this run.
- `01-tech-stack.md`, `02-basic-assessment.md` and `03-interview.md`, for the project and the user's knowledge.
- `04-curriculum.md`, the curriculum.
- Every `05-code-review-*.md` file in the folder, if there are any.
- From round 2 on: the previous lesson plan, `06-lesson-plan-r<N-1>.md`, and the review that sent it back, `07-review-r<N-1>.md`.

## Your output file

Write your output to `06-lesson-plan-r<N>.md` in the run folder the main agent gave you. `<N>` is the round number. Round 1 is your first draft. When a review sends the plan back, write the revision as a new file with the next round number, and leave the earlier rounds as they are.

Start the file with this header, and put nothing else between it and the plan's title:

```
---
step: Write the Lesson Plan
agent: tech-writer
run: <run folder name>
inputs:
  - <each file you read>
---
```

After the header, the file contains the full lesson plan, as described under *Output*, and nothing else. The plan is the one deliverable the user reads, so it holds no process record.

Write the file so that an agent who has never seen this run could continue your step from the file alone.

Append the rest to `notes.md` in the run folder, under the heading `## Write the Lesson Plan, tech-writer, round <N>`. Read `notes.md` only when the main agent's message tells you to. The entry contains:
- The files you opened.
- For each practical, the part of the Goal it advances.
- From round 2 on: a **Changes made** list. It names each change-request from `07-review-r<N-1>.md` and the text you changed in the plan.
- One section for each question you asked another agent, naming who you asked, what you asked, and the file their answer is in.
- When you answer a question as `ANSWER`, the answer goes in this entry and not in the plan file.

## Exits

- `DONE → Compare Curriculum to Task`: the lesson plan for this round is written.
- `ASK <agent>` (round trip): you need an answer to write a section. Ask the agent that owns it: the `deep-researcher` for a fact, a source, or a place in the project where a practical can apply, and the `interviewer` for whether the user already knows a topic. The agent sends you the path of its answer, and you continue writing.

## Reporting back

You are working inside the `/curriculum` process. The main agent passes your messages on exactly as you write them, and it acts only on the marker that ends your turn. End every turn with exactly one of these markers, on its own line, followed by the content that goes with it:

- `ASK USER:` followed by one question or message for the user. The user's reply comes back to you.
- `ASK <agent-name>:` followed by a question for another agent in the process: `code-recon`, `stack-advisor`, `simple-interviewer`, `interviewer`, `deep-researcher`, `code-reader`, `tech-writer` or `skeptical-student`. Name the agent that owns the answer. The answering agent records its answer in its own output file and sends you that file's path. Read the file, then continue from where you stopped.
- `ANSWER: <path>` followed, on the next line, by a one-line summary. Use this to finish every exchange that began with a question to you. First record your answer in your own output file, in a new section that names who asked and what they asked. Before answering, you may ask the user or another agent for what you need.
- `DONE → <next state>: <path>` followed, on the next line, by a one-line summary. The path is the output file you wrote for this step. Choose the next state from the Exits above, or `END` when your Exits say the process is complete.

Write your file before you send `ANSWER` or `DONE`. The main agent checks that the file exists before passing anything on.
