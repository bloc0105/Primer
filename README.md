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

**Primer** is a *Claude* based tool that reads over a codebase, and will discuss a potential task or project with you, establish the Tech stack needed to accomplish it, then asks you about your knowledge of that stack, and then finds all the documentation that fills in the gaps of your knowledge.  It's like having a private Documentation librarian that knows exactly what will help you.  

## Files 

For the complete Process, check out the [Curriculum](education/commands/curriculum.md).

Also see the [agents](education/agents) that have been created for this Tool.  

There are also two [skills](education/skills) that have been written that are used for reading a codebase.