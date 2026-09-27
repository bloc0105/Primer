---
name: basic-assessment
description: Step 2 of the /curriculum process ("Basic Assessment"). Load only when /curriculum has sent you into the "Basic Assessment" state.
user-invocable: false
---

# Basic Assessment

## Basics
- Performed by the `simple-interviewer` Agent.

## Input
The Tech Stack List from the Task Analysis

## The Process

This is an informal assessment of the skill level on the tech stack of the learner. It's simply meant to establish the level of knowledge that the user feels they have about a subject. 

## Output

A basic assessment of the user's skillset, relative to what would be necessary to complete the objectives of the proposed work on the project. 

Therefore, the List is now each subject/concept/topic/tool, plus a paragraph about how much it is used in the project, and another paragraph about how much the user knows about the subject.

## Exits

- `DONE → User Interview`: the basic assessment of every item in the Tech Stack List is complete.

## Reporting back

You are working inside the `/curriculum` process. The main agent passes your messages on exactly as you write them, and it acts only on the marker that ends your turn. End every turn with exactly one of these markers, on its own line, followed by the content that goes with it:

- `ASK USER:` followed by one question or message for the user. The user's reply comes back to you.
- `ASK <agent-name>:` followed by a question for another agent in the process: `code-recon`, `stack-advisor`, `simple-interviewer`, `interviewer`, `deep-researcher`, `code-reader`, `tech-writer` or `skeptical-student`. Name the agent that owns the answer. Its answer comes back to you, and you continue from where you stopped.
- `ANSWER:` followed by your reply to a question another agent asked you. Finish every exchange that began with a question to you this way. Before answering, you may ask the user or another agent for what you need.
- `DONE → <next state>:` followed by the finished output of your step. Choose the next state from the Exits above, or `END` when your Exits say the process is complete.
