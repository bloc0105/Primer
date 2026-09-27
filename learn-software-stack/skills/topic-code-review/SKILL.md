---
name: topic-code-review
description: Step 5 of the /curriculum process ("Topic Code Review"). Load only when /curriculum has sent you into the "Topic Code Review" state.
user-invocable: false
---

# Topic Code Review

The *Topic Research* may find what the documentation says simply does not align with the actual functionality of the subject/concept/topic/tool, or that there are different docs out there that don't agree. In this case, we must look at the source code for whatever subject/concept/topic/tool is in question to determine the truth. If there's something we don't know about SQLAlchemy, for instance, maybe we have to look at the source for it.  This should be expected to be a very rare occurrence. 

This state is not limited to resolving items Topic Research explicitly flagged as uncertain. It must also spot-check any code claim baked into the User Interview questions or Topic Research findings against the actual source, regardless of whether anyone flagged it — a confidently stated claim is not evidence it was verified. This applies with equal weight to claims embedded in an applied portion — a file path, a command, a predicted output, or a described failure mode is exactly the kind of claim this state exists to verify, and getting one wrong is worse here than in a reading list, since the user acts on it directly.

## Exits

- `ANSWER`: this state is always a round trip. `deep-researcher` asks you to check a claim. The source it names has already been prepared as plain files for you to read. Send your findings as your `ANSWER`.

## Reporting back

You are working inside the `/curriculum` process. The main agent passes your messages on exactly as you write them, and it acts only on the marker that ends your turn. End every turn with exactly one of these markers, on its own line, followed by the content that goes with it:

- `ASK USER:` followed by one question or message for the user. The user's reply comes back to you.
- `ASK <agent-name>:` followed by a question for another agent in the process: `code-recon`, `stack-advisor`, `simple-interviewer`, `interviewer`, `deep-researcher`, `code-reader`, `tech-writer` or `skeptical-student`. Name the agent that owns the answer. Its answer comes back to you, and you continue from where you stopped.
- `ANSWER:` followed by your reply to a question another agent asked you. Finish every exchange that began with a question to you this way. Before answering, you may ask the user or another agent for what you need.
- `DONE → <next state>:` followed by the finished output of your step. Choose the next state from the Exits above, or `END` when your Exits say the process is complete.
