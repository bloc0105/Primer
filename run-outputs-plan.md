# Plan: Every Step Writes an Output File

## Goal

Make each step of `/curriculum` write its result to a file inside a **run folder**. This serves two purposes:

1. **See what each agent was thinking.** Every step leaves a record of what it concluded and how it got there.
2. **Start the process anywhere.** A new run can reuse earlier steps' files and begin at any step, or run a single step on its own. For example, you can tune code discovery until it understands a codebase properly, or start research from an existing interview record.

## Guiding principles

1. **The agent doing the work writes the file.** Each agent writes its own output file, so the file is the source of truth for that step. The main agent never writes step content.
2. **Files are the source of truth; agent instances are a convenience.** Within a run, persistent agents are still resumed as before. But a step's file must hold everything a fresh agent needs to continue that step's work. That way, starting mid-process works even when the earlier agents were never started in this run.
3. **Handoffs pass file paths, not text.** `DONE → Topic Research: runs/<run>/03-interview.md`. The next agent reads the file. The main agent only passes a path on, so there's almost nothing for it to paraphrase.
4. **Each run folder is a complete snapshot.** A run that starts partway through copies in the earlier steps' files, so any two runs can be compared with `diff -r`.
5. **Every file's origin is recorded.** A `run.md` manifest records which files were copied in, from which run, and which were produced by this run.

## Run folder layout

```
runs/
  2026-09-27-fix-login-bug/
    run.md                      # manifest: request, mode, origin of every file
    01-tech-stack.md            # code-recon or stack-advisor
    02-basic-assessment.md      # simple-interviewer
    03-interview.md             # interviewer
    04-curriculum.md            # deep-researcher
    05-code-review-<topic>.md   # code-reader, OPTIONAL: zero or more, one per question it was asked
    06-lesson-plan-r1.md        # tech-writer, one file per revision round
    07-review-r1.md             # skeptical-student, one file per review round
    06-lesson-plan-r2.md
    07-review-r2.md
    ...
```

The numbers follow step order, so "every file numbered below N" is exactly the set of inputs for step N. Code-review files are numbered 05 because they're produced during research and feed into writing.

**Code review is optional.** It only happens when the researcher asks `code-reader` to check a claim, and most runs won't have any `05-` files at all. Nothing downstream expects them. A run with no `05-` files is complete, and a `--from` start copies whatever `05-` files the source run has, which is often none.

Lesson plans and reviews get one file per round, rather than being overwritten, so you can see how the plan changed in response to each review.

Run folders are named `<date>-<short-slug-of-the-request>`. If a folder with that name already exists, a `-2`, `-3` etc. is added.

## What goes in each file

Each file starts with a short header: the step name, the agent, the run, and the input files it read. After that, it has the output, and then a **How I got here** section in which the agent explains its reasoning. That section is what covers goal 1.

| File | Must contain, so a fresh agent can continue from it |
|---|---|
| `01-tech-stack.md` | The Tech Stack List as the step defines it, plus any bugs or deprecated patterns `code-recon` flagged. For Proposal Mode, also the user's confirmations and objections. |
| `02-basic-assessment.md` | Every question asked and the user's answer, word for word, plus the assessment. |
| `03-interview.md` | Every question and the user's answer, word for word, plus the final assessment, with concept knowledge and vocabulary kept separate. Follow-up interviews add a new section that names who asked and why. The earlier record is left unchanged. If there are follow up questions, they need to be apended on. |
| `04-curriculum.md` | The ordered curriculum, plus the sources that were considered and why each was chosen or dropped. |
| `05-code-review-<topic>.md` *(optional)* | The claim that was checked, the source that was read (repo, version or branch, files), and the findings. |
| `06-lesson-plan-rN.md` | The full lesson plan for round N. Round 1 is the first draft. Every later round is a revision that answers the previous review (`07-review-r<N-1>.md`), so it also includes a **Changes made** list: each change-request from that review, and what the tech-writer changed in response. |
| `07-review-rN.md` | Approval, or the list of change-requests, for round N. |

## The run manifest (`run.md`)

The main agent writes this file. It contains only setup facts, never step content:
- **Request:** the user's request, word for word. Every agent reads it to learn what the project is. Today that only exists in the main agent's context.
- **Mode:** `full`, `from <step>`, or `only <step>`.
- **Source run:** the run files were copied from, if any.
- **Files:** one line per file saying whether it was **copied from `<run>`** or **produced by this run**. The main agent adds a line each time an agent reports a file.

## The transcript (`transcript.md`)

The main agent also keeps a word-for-word log of every message it passes on: each `ASK USER`, the user's reply, each `ASK <agent>`, `ANSWER` and `DONE`, in order, each labelled with who sent it and who received it. The step files show what each agent concluded and why. The transcript shows the conversation between agents that led there. The main agent only appends exact messages to it and never adds wording of its own.

## Starting modes

```
/curriculum <request>                                  # full run, new folder
/curriculum --from <step> <source-run> [notes]         # new folder, copy earlier files, run from <step> to END
/curriculum --only <step> <source-run> [notes]         # new folder, copy earlier files, run just <step>, then stop
```

- `<step>` is the step's skill name, for example `topic-research` or `discover-stack`.
- **What gets copied:** files numbered *below* the starting step, plus the request from the source run's `run.md`. Files at or after the starting step are never copied, so nothing old can be mistaken for new output.
- **`topic-code-review` is not a starting step.** Code review only happens when the researcher asks `code-reader` to check a claim, so there's nothing to start it with. If someone passes it to `--from` or `--only`, the main agent tells the user so and stops without creating a run folder. To tune code review, run `--only topic-research` on a request where the documentation is known to be wrong, so the researcher has a reason to ask.
- **`[notes]`** is optional text telling the agent what's being tuned. It's recorded in `run.md` so you can find the run later.
- **`--only`** stops when the step's agent sends `DONE`. Round trips still work in this mode: if the researcher asks the interviewer a question, the interviewer is started, reads `03-interview.md`, and updates it in the new folder. Those changes are what `diff -r` will show.

## Changes to the plugin

### `commands/curriculum.md`
- **Argument parsing and run setup:** read the mode, create the run folder, copy the earlier files, and write `run.md`.
- **State table:** add a column for the output file of each state.
- **Starting an agent:** give it the run folder path and the paths of its input files, not their contents.
- **When an agent reports `DONE`, `ANSWER` or a written file:** record the file in `run.md`, then pass on the path.
- **Hard rule 4** becomes: "Leave all content writing to the agents. Your file operations are setting up the run folder, keeping `run.md` up to date, appending exact messages to `transcript.md`, and *Preparing source*."
- **Checking for missing files:** when an agent sends `DONE` or `ANSWER`, check that the file it named exists. If it doesn't, send the agent back to write it before passing anything on, the same way a turn with no marker is handled.

### Each step skill
- A new **Your output file** section. It gives the file name, what the file must contain (from the table above), the header, and the How I got here section.
- A new **Your input files** section that lists which earlier files to read.
- **Reporting back** changes: `DONE` and `ANSWER` carry the path of the file written, followed by a one-line summary.
- **Interview skills:** record every question and answer in the file as the interview goes. That way the record survives even if the run stops partway through.

### Agents' `tools:` lists
Every agent needs `Read` to read its inputs, and `Write` to write its output. The interviewer also needs `Edit` to add follow-up sections.

| Agent | Adds |
|---|---|
| `stack-advisor`, `simple-interviewer`, `deep-researcher` | `Read`, `Write` |
| `interviewer` | `Read`, `Write`, `Edit` |
| `code-recon`, `code-reader`, `skeptical-student` | `Write` |
| `tech-writer` | already has these |

`code-reader` and `skeptical-student` keep their rule against producing replacement documents. A findings or review file is their report, not a rewrite of the material they reviewed.

### Where runs live
- Runs are created in `./runs/`, in whatever directory Claude was launched from.
- The first time the main agent creates `runs/`, it also writes `runs/.gitignore` containing `*`. This makes the folder ignore itself in any git repo, without editing that repo's own `.gitignore`. Outside a git repo the file does nothing.

## Execution order

1. Write the "Your output file" and "Your input files" text once, as a template, then fill it in for each step.
2. Update the Reporting back section in all 8 step skills.
3. Update the agents' `tools:` lists.
4. Update `curriculum.md`: run setup, argument parsing, the state table column, how agents are started, and hard rule 4.
5. Run `claude plugin validate`.
6. **Dry run 1:** a full run on a small request. Check that every file is written, `run.md` and `transcript.md` are accurate, each file stands on its own, and `git status` doesn't show `runs/`.
7. **Dry run 2:** `--from topic-research` using the run from dry run 1. Check that only files 01–03 are copied, and that a researcher question reaches a fresh interviewer, which then updates `03-interview.md`.
8. **Dry run 3:** `--only discover-stack` on the same request, then `diff -r` it against dry run 1.
9. Commit on `adb-testing`.

## Decisions

1. **Where runs live:** `./runs/`, in the directory Claude is launched from.
2. **Git:** if that directory is in a git repo, `runs/` is ignored, through a `.gitignore` inside `runs/` itself.
3. **Transcript:** yes. The main agent keeps a word-for-word `transcript.md`.
4. **Missing files:** the main agent sends the agent back to write the file before passing anything on.
