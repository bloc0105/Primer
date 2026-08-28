---
name: curriculum
description: The process to establish what the users path will be to learn a new subject or codebase.
---

# Overall

This is a command to establish a learning plan to bridge the gap from what they know to what they don't

# The Process


## Step 1. Assessment of the Subject

The AI will establish what the user is trying to achieve. It might be something like:

- Being able to understand a codebase.
- Fixing a bug in an existing codebase.
- Building a new application from scratch.
- Learning a new software tool.

The user will form their request as a prompt entered as a parameter to this command. If the user doesn't provide a prompt, ask them what they're looking to do.

**First, determine the mode:**

- If the user references existing code (a repo, a file path, a specific bug, "help me understand/fix X"), this is **Discovery Mode**. Invoke the `discover-stack` skill.
- If the user describes a goal with no existing code ("I want to build X"), this is **Proposal Mode**. Invoke the `propose-stack` skill.
- If the request is ambiguous, ask the user directly which situation applies before proceeding.

Both skills produce the same output: a **Tech Stack List**, the set of software components, tools, and concepts that make up the system, i.e. everything someone would need to know in order to work on it. This list is what Steps 2 through 4 operate on, regardless of which mode produced it.

Do not proceed to Step 2 until the Tech Stack List has been produced and, in Proposal Mode, confirmed by the user.

Output: Tech Stack List

## Step 2. Assessment of the User's knowledge base

Once the Tech Stack has been established, it's time to see how well the user knows it.  At this point, the AI should ask the user questions that determine how well the user knows what something does.  This could be any series of questions ranging from "what does this code do?" and showing a snippet or "Write a function in Java that does ____" or it could even involve "What's the derivative of $x^2$ in terms of $x$.  The questions are entirely at the discretion of the AI, as long as they determine how well the user knows the system.  The AI may ask any number of questions, and these question should not feel like the user is getting "tested" or "grilled" but more like "here, let's see what you know so that I can help fill in the blanks for you". 

Output: List of what the user knows about each component of the tech stack and what they don't.

## Step 3. The Search

The AI then goes out and does research on each software component. The research process will consist of at least the following

- Reading the online documentation on the component. 
- Reading the Forums or articles on the component. 
- Reading source code for the component, if available.  

The research process will likely be recursive. eg: in order to know PostGres, you need to know SQL.  So the AI can stop the research once they've reached something the user knows.

Output: List of all the pertinent documentation to the tech stack, relative to the user's knowledge base. 

## Step 4. Forming the List

The final step is to form a curriculum of what the user has to do in order to learn each software component and in what order.  There's a certain complexity here. The AI needs to 

- Take the information that has been gathered. 
- Take the user's knowledge about each software component.  
- Cross reference each of the and establish what the user needs to do 
    - What parts of the documentation do they need to read?
    - What tutorials will help them learn?
    - After the reading and tutorials, how can they **immediately** apply their newly found skills to the problem that they originally faced.  

For Example, a learning plan might look something like this:

1. Read PostGres Chapter 1.
1. Perform the Postgres tutorial included in Chapter 1.
    - Apply what you learned to line __ in file ___.py in order to apply this to your problem.
1. Read Postgres Chapter 4. 
    - Apply what you learned to the application in order to fix _____ bug.  

And it continues from there until everything the user would need to know is stacked into a curriculum they can follow.  

Note that there could be steps in the learning that are skipped if the user already knows them.

The ordering has to respect prerequisite structure, not just be freeform,so that the user can follow the curriculum exactly. 

Output: The curriculum for the user to follow. 

## Iteration Process

The *Step 2. Assessment of the User's knowledge base*  and *Step 3. The Search* could potentially iterate back and forth if the research uncovers something that needs to be assessed against the user's knowledge.  

There are a couple of possibilities that could happen as the research carries on through these iterations. 

The stopping side: at some point a node's depth exceeds what's actually load-bearing for the goal. You don't need to understand how the C compiler translates to assembly to write C, you just need to trust it works. It's a key distinction between *user* and *developer*.  Once you reach the user level, you don't need to keep going to the developer level. 

The expansion side: a node turns out to have a prerequisite that's actually necessary, not just interesting, and skipping it would mean the person hits a wall later that the curriculum should have prevented. This is the case where the loop between assessment and search genuinely needs to add a new node to the map rather than close one out.