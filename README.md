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

**Primer** is a *Claude* based tool that reads over a codebase and works out, with you, exactly what has to change to get you what you want. Once you've agreed on those changes, it works out what you need to learn to make them yourself, asking you about your knowledge along the way, and finds the documentation that fills in the gaps. It's like having a private Documentation librarian that knows exactly what will help you.

It works whether you're diving into an existing codebase or starting something new. If there's no code yet, Primer chooses the tools as part of planning the changes.

What you get at the end is a **lesson plan**. Every unit pairs the reading you actually need with a step of the changes you agreed to, in *your* project, so you're moving your real work forward while you learn. Before you see it, a separate reviewer checks the plan: is everything in the right order, does each step use what you just read, does every step belong to a change you agreed to, and is it pitched at your level?

## How it works

Primer moves between states. Each state hands off to another when its work is done, or calls on another when it needs something.

- **Task Analysis.** Tell Primer what you want to do. If there's a codebase, it reads what the code does now.
- **Define Product Changes.** Plans what the finished product does, and the changes that get there. Only what your goal needs, plus anything it recommends for security.
- **Review Product Changes.** A separate reviewer checks that every change is needed for that finished product, so nothing extra reaches you or the lessons.
- **Basic Assessment.** A quick, informal conversation about the tools and ideas those changes involve. If a revised list brings in something new, it asks about just that.
- **Confirm Product Changes.** Explains the finished product and the changes in your words, and asks you the two things only you can decide: is that finished product what you want, and do you want each security recommendation, explained by what could happen without it. You aren't asked to judge the technical changes; the reviewer already has. If the finished product isn't what you want, say so, and the list is revised.
- **Topic Research.** Works backward from what the changes need. Whenever it reaches something it can't tell whether you know, it calls on **Interview Question**, which asks you one pointed question about it, and research then goes further back or stops. When the docs disagree with each other or with reality, it calls on **Topic Code Review**, which reads the actual source code to settle it. If it finds a change can't be made as planned, the list goes back to be amended and reviewed, and comes back to you only if what the finished product does would change. Research ends where what the changes need meets what you already know.
- **Write the Lesson Plan.** Turns the research into lessons. Each lesson ends with a step of the agreed changes, one you can see working on its own, and builds as much as its reading allows. When it needs more information, it asks Topic Research.
- **Compare Curriculum to Task.** A skeptical reviewer checks the plan against the agreed changes and sends it back to the writer until it's right.

The agent that plans the changes is never the one that checks them or explains them to you, and the agent that writes the lesson plan is never the one that approves it.

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
