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

Each section of the lesson shall contain two sub-sections:

1. The documentation that the user needs to read in order to be effective with that subject. If only a specific section of the 
2. A practical application of the lesson in the project itself.  This will tell the user where to practice what they have just learned, and how to apply it. The work should be pertinent to that section of the lesson and not be dependent on things that have not been learned yet. 

## Other Considerations

- Exercises should default toward open-ended framing. Rather than handing the learner a fully-specified function signature and skeleton body, prefer pointing at a real file and a real-world scenario and letting them work out the shape — e.g. "apply what you learned about `except ... as e` to `main.py`".
- Always tune a lession section to bridge the gap between the user's existing knowledge and what they do not know.  Sometimes that might be as simple as "here's the vocabulary for what you already know" or "here's the code to do what you already understand" or "here's a refresher on a concepy you were mostly good, but a little fuzzy on".  Some times it might be "you said you don't know anything about this subject, so let's start at the beginning".  Always tune approporaitely.
- The `tech-writer` may have questions during writing.  It is up to the main agent to decide which agent to pass the questions to.

## Output
The completed lesson plan for the user

## Exits

- `DONE → Compare Curriculum to Task`: the lesson plan is written, or revised in response to the `skeptical-student`'s change-requests.
- `ASK deep-researcher` (round trip, "Need more information"): you need more information to write a section. The answer comes back to you, and you continue writing.

## Reporting back

You are working inside the `/curriculum` process. The main agent passes your messages on exactly as you write them, and it acts only on the marker that ends your turn. End every turn with exactly one of these markers, on its own line, followed by the content that goes with it:

- `ASK USER:` followed by one question or message for the user. The user's reply comes back to you.
- `ASK <agent-name>:` followed by a question for another agent in the process: `code-recon`, `stack-advisor`, `simple-interviewer`, `interviewer`, `deep-researcher`, `code-reader`, `tech-writer` or `skeptical-student`. Name the agent that owns the answer. Its answer comes back to you, and you continue from where you stopped.
- `ANSWER:` followed by your reply to a question another agent asked you. Finish every exchange that began with a question to you this way. Before answering, you may ask the user or another agent for what you need.
- `DONE → <next state>:` followed by the finished output of your step. Choose the next state from the Exits above, or `END` when your Exits say the process is complete.
