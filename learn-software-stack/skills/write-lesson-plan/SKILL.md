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

The lesson plan shall read as a textbook for a general audience that happens to have one reader. Each of these shall be true of the plan file, and each can be checked by searching it:

1. It does not mention the interview, a review, a revision round, or how the plan was made.
2. It does not contain "you" or "your", outside quotations.
3. Every label, abbreviation and term of art it uses is defined in the plan, or is standard in the field.
4. An analogy to a language or tool the reader knows is written in the abstract ("similar to Java static class variables"), without reference to the reader.

Each section of the lesson shall contain two sub-sections:

1. The documentation that the user needs to read in order to be effective with that subject. If only a specific section of the 
2. A practical application of the lesson in the project itself.  This will tell the user where to practice what they have just learned, and how to apply it. The work should be pertinent to that section of the lesson and not be dependent on things that have not been learned yet. 

## Other Considerations

- Exercises should default toward open-ended framing. Rather than handing the learner a fully-specified function signature and skeleton body, prefer pointing at a real file and a real-world scenario and letting them work out the shape — e.g. "apply what you learned about `except ... as e` to `main.py`".
- Always tune a lession section to bridge the gap between the user's existing knowledge and what they do not know.  Sometimes that might be as simple as "here's the vocabulary for what you already know" or "here's the code to do what you already understand" or "here's a refresher on a concepy you were mostly good, but a little fuzzy on".  Some times it might be "this section starts at the beginning, with no assumed background".  Always tune approporaitely, and keep the wording within the rules above: the tuning shows in what the section covers, never in addressing the reader or retelling what they said.
- The `tech-writer` may have questions during writing.  It is up to the main agent to decide which agent to pass the questions to.

## Output
The completed lesson plan for the user

## Your input files

The main agent gives you the path of the run folder. Read these files from it before you begin:
- `run.md`, for the user's request (the **project**) and any notes about this run.
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
- What you looked at, what you weighed, and why you decided as you did.
- From round 2 on: a **Changes made** list. It names each change-request from `07-review-r<N-1>.md` and says what you changed in response.
- One section for each question you asked another agent, naming who you asked, what you asked, and the file their answer is in.
- When you answer a question as `ANSWER`, the answer goes in this entry and not in the plan file.

## Exits

- `DONE → Compare Curriculum to Task`: the lesson plan for this round is written.
- `ASK deep-researcher` (round trip, "Need more information"): you need more information to write a section. The researcher sends you the path of its answer, and you continue writing.

## Reporting back

You are working inside the `/curriculum` process. The main agent passes your messages on exactly as you write them, and it acts only on the marker that ends your turn. End every turn with exactly one of these markers, on its own line, followed by the content that goes with it:

- `ASK USER:` followed by one question or message for the user. The user's reply comes back to you.
- `ASK <agent-name>:` followed by a question for another agent in the process: `code-recon`, `stack-advisor`, `simple-interviewer`, `interviewer`, `deep-researcher`, `code-reader`, `tech-writer` or `skeptical-student`. Name the agent that owns the answer. The answering agent records its answer in its own output file and sends you that file's path. Read the file, then continue from where you stopped.
- `ANSWER: <path>` followed, on the next line, by a one-line summary. Use this to finish every exchange that began with a question to you. First record your answer in your own output file, in a new section that names who asked and what they asked. Before answering, you may ask the user or another agent for what you need.
- `DONE → <next state>: <path>` followed, on the next line, by a one-line summary. The path is the output file you wrote for this step. Choose the next state from the Exits above, or `END` when your Exits say the process is complete.

Write your file before you send `ANSWER` or `DONE`. The main agent checks that the file exists before passing anything on.
