# Primer
A Claude Plugin that helps you set up a curriculum, and execute the curriculum, teaching you along the way. 

## The Gap

We've all been there.  You want to make a big splash in the open-source world.  Maybe there's some awesome tool that you use all the time, and you want to add features to it.  Maybe you found a bug you'd like to fix. Or maybe you have an idea for something cool you want to build.  

Then you try to dive in and you're hit on the head by cruel reality. The tool is written in a language you barely know.   On top of that, it has dependencies on other libraries you've never even heard of. And it's built using a tool you used one time and never learned.  And **Wait, who is Kubernetes?**

What are we always told? **RTFM!** You gotta go read the Docs to the various software tools. Learn how to put it all together, and then you can make your contribution.  But the reality is most documentation is scattered throughout the internet. Usually there's a documentation page, but it's out of date or incomplete. Or you go to a forum, or maybe you get lucky and know somebody.  And all of this takes years just to learn enough to make one contribution.

And a huge amount of that time is wasted.  You don't need to read *every* chapter of a demo document, just to learn the basics. 

And for people who really want to dig in and learn, there's just no way to do it all. 

There should be a better way. 

## The Fill

**Primer** is a *Claude* based tool that reads over a codebase, and will discuss a potential task or project with you, establish the Tech stack needed to accomplish it, then works out what you need to learn, asking you about your knowledge along the way, and finds the documentation that fills in the gaps.  It's like having a private Documentation librarian that knows exactly what will help you.  

It works whether you're diving into an existing codebase or starting something new. If there's no code yet, Primer recommends a tech stack for your idea first.

What you get at the end is a **lesson plan**. Every section pairs the reading you actually need with a hands-on exercise in *your* project, so you're moving your real work forward while you learn. Before you see it, a separate reviewer checks the plan: is everything in the right order, does each exercise use what you just read, and is it pitched at your level?

## How it works

Primer moves between states. Each state hands off to another when its work is done, or calls on another when it needs something.

- **Task Analysis.** Tell Primer what you want to do. It reads your codebase, or proposes a stack for a new project, and lists everything the work involves.
- **Basic Assessment.** A quick, informal conversation about what you already know.
- **Topic Research.** Works backward from what the task needs. Whenever it reaches something it can't tell whether you know, it calls on **Interview Question**, which asks you one pointed question about it, and research then goes further back or stops. When the docs disagree with each other or with reality, it calls on **Topic Code Review**, which reads the actual source code to settle it. Research ends where what the task needs meets what you already know.
- **Write the Lesson Plan.** Turns the research into lessons, each with an exercise in your project. When it needs more information, it asks Topic Research.
- **Compare Curriculum to Task.** A skeptical reviewer checks the plan and sends it back to the writer until it's right.

Each state is run by its own agent, so the agent that writes the lesson plan is never the one that approves it.

## Installation

In Claude Code:

```
/plugin marketplace add bloc0105/Primer
/plugin install learn-software-stack@Primer
```

Then start a curriculum by describing what you want to do:

```
/learn-software-stack:curriculum I want to fix the login bug in ~/code/my-app
```

## Files

- [Curriculum](learn-software-stack/commands/curriculum.md): the full process, and the rules for how the states connect.
- [Agents](learn-software-stack/agents): one agent for each role in the process.
- [Skills](learn-software-stack/skills): one skill for each state, holding the instructions its agent follows.
