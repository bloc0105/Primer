---
name: topic-research
description: Step 4 of the /curriculum process ("Topic Research"). Load only when /curriculum has sent you into the "Topic Research" state.
user-invocable: false
---

# Topic Research

## Basics
- Performed by the `deep-researcher` Agent.

## Input
The Interview results with each subject/concept/topic/tool, and the user's knowledge of it. 

## The Process
Now the task is the research on each subject/concept/topic/tool to establish the curriculum of documentation that the user would need to get from their current state of knowledge, to the state of knowledge necessary to complete the work for the project.  The following are some of the place that the researcher could go in order to 

- Reading the online documentation on the component from the official website. 
- Reading the Forums or articles on the component. 

The research process will likely be recursive. eg: in order to know Postgres, you need to know SQL.  So the research can stop once it crosses into the knowledge base of the user.

It may be possible that the *Topic Research* process discovers further prerequisites to a given subject/concept/topic/tool.  This could be either a situation where a new prerequisite subject/concept/topic/tool is discovered, or there is simply more information about the subject/concept/topic/tool that wasn't assessed relative to the user's knowledge. In either case, it may be necessary to go back to the *User Interview* and ask more questions to the user. This loop-back shall resume the same `interviewer` agent instance used for the original interview, not spawn a new one — the agent needs the full history of prior answers to fold the new question into one coherent determination, rather than producing a second, disconnected assessment.

## Output
The list of Documentation that is necessary to get the user from their current state to the state in which they know enough to complete the task for the project. This will be referred to as the curriculum. The curriculum shall be in an order in which the human user is expected to read the material. This means that no subject shall contain material that has not been learned in a previous subject.

## Exits

- `DONE → Write the Lesson Plan`: the research is compiled into the curriculum.
- `ASK interviewer` (round trip, "Sub-Topic Discovered"): you found a prerequisite, or more about a subject/concept/topic/tool, that the interview did not assess. Name the sub-topic. The interviewer's determination comes back to you, and you continue your research.
- `ASK code-reader` (round trip, "Something's wrong with Doc"): the documentation disagrees with itself or with how the subject/concept/topic/tool actually behaves. Name the repository (with a URL), the version or branch, and the exact claim to check. The code-reader's findings come back to you, and you continue your research.
- `ANSWER`: when `tech-writer` asks you for more information, research it and send what you found as your `ANSWER`.

## Reporting back

You are working inside the `/curriculum` process. The main agent passes your messages on exactly as you write them, and it acts only on the marker that ends your turn. End every turn with exactly one of these markers, on its own line, followed by the content that goes with it:

- `ASK USER:` followed by one question or message for the user. The user's reply comes back to you.
- `ASK <agent-name>:` followed by a question for another agent in the process: `code-recon`, `stack-advisor`, `simple-interviewer`, `interviewer`, `deep-researcher`, `code-reader`, `tech-writer` or `skeptical-student`. Name the agent that owns the answer. Its answer comes back to you, and you continue from where you stopped.
- `ANSWER:` followed by your reply to a question another agent asked you. Finish every exchange that began with a question to you this way. Before answering, you may ask the user or another agent for what you need.
- `DONE → <next state>:` followed by the finished output of your step. Choose the next state from the Exits above, or `END` when your Exits say the process is complete.
