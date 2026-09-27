---
name: user-interview
description: Step 3 of the /curriculum process ("User Interview"). Load only when /curriculum has sent you into the "User Interview" state.
user-invocable: false
---

# User Interview

## Basics
- Performed by the `interviewer` Agent.

## Input
The Basic Assessment of the learner's skill-set.

## The Process

The purpose of the basic assessment was to determine roughly what the user knows about a subject. Now is the point to narrow that understanding with precision.

At this point, the user is interviewed to determine their knowledge of the various subjects/concepts/topics/tools. The interview shall be invoked iteratively: one question per call, with the main agent relaying that question to the user, then relaying the user's answer back to that same agent instance before requesting the next question. 

Since the basic assessment already covered some topics, the interview should account for this, which will expedite the interviewer process.  For instance, if the user explicitly said they know nothing about a certain subject/concept/topic/tool, it's probably not necessary to ask them about it.  

The main agent does not choose what to ask, interpret an answer, or decide when the interview ends — that authority belongs to the `interviewer` agent alone, which also produces the final determination itself, from having tracked the interview throughout, rather than the AI reconstructing it afterward.

The `interviewer` may, however, need to establish relevance of its questions to the project itself, and should be asking the main agent, who may forward questions to other agents, whether it's question has pertinence, so as to not ask questions that have no bearing on the project. 

## Output

This will be the same list as the list that was established by the basic assessment, but with significantly more precision, describing exactly which sub-topics of a subject/concept/topic/tool the user is familiar with, and where the gaps lie. The user's conceptual knowledge will be separate from their vocabulary knowldge.  This means that if a user knows how to do something, but doesn't know the terminology for it, this is considered different from actually not knowing the subject/concept/tool/topic.  From this, the interview can tell exactly what things the user must learn in orer to complete the work necessary to accomplish the objectives of the project.

## Exits

- `DONE → Topic Research`: the interview is complete and the user is assessed.
- `ANSWER`: when `deep-researcher` asks you about a newly discovered sub-topic, interview the user about it with `ASK USER` turns, then send your updated determination for that sub-topic as your `ANSWER`.

## Reporting back

You are working inside the `/curriculum` process. The main agent passes your messages on exactly as you write them, and it acts only on the marker that ends your turn. End every turn with exactly one of these markers, on its own line, followed by the content that goes with it:

- `ASK USER:` followed by one question or message for the user. The user's reply comes back to you.
- `ASK <agent-name>:` followed by a question for another agent in the process: `code-recon`, `stack-advisor`, `simple-interviewer`, `interviewer`, `deep-researcher`, `code-reader`, `tech-writer` or `skeptical-student`. Name the agent that owns the answer. Its answer comes back to you, and you continue from where you stopped.
- `ANSWER:` followed by your reply to a question another agent asked you. Finish every exchange that began with a question to you this way. Before answering, you may ask the user or another agent for what you need.
- `DONE → <next state>:` followed by the finished output of your step. Choose the next state from the Exits above, or `END` when your Exits say the process is complete.
