---
name: write-lesson-plan
description: The "Write the Lesson Plan" state of the /curriculum process. Load only when /curriculum has sent you into the "Write the Lesson Plan" state.
user-invocable: false
---

# Write the Lesson Plan

## Basics

- Performed by the `tech-writer` Agent.

## Input

- The accepted changes.
- The curriculum from the Research State, with each change's subject list.
- The interview assessment of the user.

## The Process

This is where the lesson plan is actually created.

The lesson plan shall be a list of citations to documentation, plus a practical for each unit. The documentation teaches, and the plan says what to read. Each of these shall be true of the plan file, and each can be checked by searching it:

1. It does not mention the interview, a review, a revision round, or how the plan was made.
2. It does not contain "you" or "your", outside quotations.
3. Every item in a Vocabulary or Reading sub-section is one citation.
4. Each citation carries at most one line of the plan's own words, a `Covers:` bullet saying what the learner gets from it.
5. No Vocabulary or Reading sub-section contains a code block, definition or analogy that the plan wrote. A definition is quoted verbatim from its source, with a link.

**One exception.** When the cited documentation is wrong for this project, or does not explain something the learner needs, a citation may carry a `Note:` bullet of two sentences or fewer, placed under the section it corrects. The note says what is wrong or missing and what is true instead. Your `notes.md` entry lists each note with the reason.

Each unit of the lesson shall contain three sub-sections, in this order:

1. **Vocabulary:** each term that the unit's readings use, that the learner needs, and that the interview assessment does not show the user already using correctly. Each entry is the term in bold, with the defining sentence quoted from its source and a link to that source as bullets under it, all taken from the Terms of the curriculum entries the unit covers. A second quote is a second bullet. A term appears in the unit where it is first needed and nowhere else. When the curriculum has no source for a term, or says no source defines it, `ASK deep-researcher` for one before writing a correction note. A unit that needs no terms says so.
2. **Reading:** the documentation that the user needs to read in order to be effective with that subject. If only a specific section of a page is what the user doesn't already know, assign that section and not the whole page, and say which one.
3. **Practical:** the steps of the accepted changes that the unit's last entry completes, as described below.

Each reading item shall satisfy every rule below, and each is a yes/no test:

1. The page is a numbered item with its link. Under it, the sections to read are a nested numbered list, by heading or section number, with subsections nested under their parent.
2. It names what to read by section number or heading, and does not describe how the page looks (a box, a sidebar, a table).
3. Anything in an assigned section that the learner does not need, and that no Vocabulary entry defines, is a `Skip:` bullet under that section. When it covers the whole page, the bullet goes under the page. The curriculum entry's Ignorable list is where to start.

The Vocabulary and Reading sub-sections take this shape:

```markdown
### Vocabulary

- **<term>**
  - "<defining sentence, quoted verbatim>"
  - [<Source>, <Page>](<link>)

### Reading

1. [<Source>, <Page>](<link>)
   1. <Section heading or number>
      1. <Subsection heading or number>
      - Skip: <what in this section can be ignored>
   2. <Section heading or number>
      - Note: <what the documentation gets wrong or leaves out here, and what is true instead>
   - Skip: <what on the whole page can be ignored>
   - Covers: <what the learner gets from this reading>
```

The plan shall begin with Unit 0, whose practical is running the project as it stands and demonstrating how it works. Unit 0 includes the setup needed to run the project only when the interview assessment shows the user cannot run it already. Its Vocabulary and Reading sub-sections are whatever the user needs to run the project at all, and either may say that none is needed. The practical rules below apply from Unit 1 on, not to Unit 0.

Units follow the curriculum's order. A unit ends at an entry that completes at least one step, and teaches that entry together with every earlier entry no unit has taught yet. Its practical holds every step that entry completes.

Each practical step is part of an accepted change, and takes this shape:

> Currently \<what the project does now\>, in \<the file or area where it is\>. Make it so that \<what it does instead\>.
> - Change: \<the accepted change it is part of\>

Each step satisfies every rule below, and each is a yes/no test:

1. It is part of one accepted change, and names it.
2. It is in the unit whose last entry completes its needs.
3. It says what the project currently does, names the file or area, and says what it does instead, leaving the method to the learner.
4. Its "Make it so that" names something the running project then does that the learner can see, with this step alone. A step whose effect can only be seen after a later step is combined with that step, in that step's unit.
5. It states no result: no command to run, no output, status code or test outcome to compare against.
6. It uses only subjects taught in this unit or earlier.

The steps of each accepted change together make the whole change, and no more. By the last unit, every accepted change is complete.

## Other Considerations

- Tune each unit to the user's knowledge by what it assigns, lists and skips: which terms, which sections, where to stop, what to ignore. Never by writing explanation, and never by addressing the reader or retelling what they said.
- Stay inside the curriculum and the accepted changes. Something worth teaching or fixing that no accepted change needs stays out. When an accepted change can't be made with what the curriculum teaches, `ASK deep-researcher`. Ask the `deep-researcher` too for a fact, a source, or whether the user already knows a topic. Asking costs nothing, and guessing does.
- The `tech-writer` may have questions during writing.  It is up to the main agent to decide which agent to pass the questions to.

## Output
The completed lesson plan for the user

## Your input files

The main agent gives you the path of the run folder. Read these files from it before you begin:
- `run.md`, for the **Goal** (the **project**) and any notes about this run.
- The `product-changes-r<N>.md` and `product-changes-explained-r<N>.md` with the highest round number: the accepted changes, minus any recommended change the user dropped.
- `current-code.md`, when there is a codebase.
- `basic-assessment.md` and `interview.md`, for the user's knowledge.
- `curriculum.md`, the curriculum.
- Every `code-review-*.md` file in the folder, if there are any.
- When a review has sent the plan back: the previous lesson plan, `lesson-plan-r<N-1>.md`, and the review that sent it back, `review-r<N-1>.md`.

## Your output file

Write your output to `lesson-plan-r<N>.md` in the run folder the main agent gave you. `<N>` is the round number. Round 1 is your first draft. When a review sends the plan back, write the revision as a new file with the next round number, and leave the earlier rounds as they are.

Start the file with this header, and put nothing else between it and the plan's title:

```
---
state: Write the Lesson Plan
agent: tech-writer
run: <run folder name>
inputs:
  - <each file you read>
---
```

After the header, the file contains the full lesson plan, as described under *Output*, and nothing else. The plan is the one deliverable the user reads, so it holds no process record.

Write the file so that an agent who has never seen this run could continue your work in this state from the file alone.

Append the rest to `notes.md` in the run folder, under the heading `## Write the Lesson Plan, tech-writer, round <N>`. Read `notes.md` only when the main agent's message tells you to. The entry contains:
- The files you opened.
- When a review has sent the plan back: a **Changes made** list. It names each change-request from `review-r<N-1>.md` and the text you changed in the plan.
- One section for each question you asked another agent, naming who you asked, what you asked, and the file their answer is in.
- When you answer a question as `ANSWER`, the answer goes in this entry and not in the plan file.

## Exits

- `DONE → Compare Curriculum to Task`: the lesson plan for this round is written.
- `ASK <agent>` (round trip): you need an answer to write a section. Ask the agent that owns it: the `deep-researcher` for a fact, a source, or whether the user already knows a topic. The agent sends you the path of its answer, and you continue writing.

## Reporting back

You are working inside the `/curriculum` process. The main agent passes your messages on exactly as you write them, and it acts only on the marker that ends your turn. End every turn with exactly one of these markers, on its own line, followed by the content that goes with it:

- `ASK USER:` followed by one question or message for the user. The main agent shows it to the user and sends you their reply word for word. That reply is the user's answer: record it as theirs.
- `ASK <agent-name>:` followed by a question for another agent in the process: `code-recon`, `stack-advisor`, `simple-interviewer`, `interviewer`, `deep-researcher`, `code-reader`, `tech-writer` or `skeptical-student`. Name the agent that owns the answer. The answering agent records its answer in its own output file and sends you that file's path. Read the file, then continue from where you stopped.
- `ANSWER: <path>` followed, on the next line, by a one-line summary. Use this to finish every exchange that began with a question to you. First record your answer in your own output file, in a new section that names who asked and what they asked. Before answering, you may ask the user or another agent for what you need.
- `DONE → <next state>: <path>` followed, on the next line, by a one-line summary. The path is the output file you wrote in this state. Choose the next state from the Exits above, or `END` when your Exits say the process is complete.

Write your file before you send `ANSWER` or `DONE`. The main agent checks that the file exists before passing anything on.
