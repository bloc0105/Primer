---
name: curriculum
description: The process to establish what the users path will be to learn a new subject or codebase.
---

# Overall

This is a command to establish a learning plan to bridge the gap from what they know to what they don't

# Agents

The AI may use the best Agent to complete a task. 

# The Process


## Step 1. Assessment of the Subject

The AI will establish what the user is trying to achieve.  It might be something like:

- Being able to understand a codebase.
- Building a new application from scratch.
- Learning a new software tool.

The user will form their request as a prompt that is entered as a parameter to this command. IF the user doesn't put in a prompt, ask them what they're looking to do. 


The job of the AI is to establish all of the software packages that are involved in that software package.  For example, if it's a web framework, and it uses JQuery, Flask, and Postgres, each of those components **might** be something the user has to learn.  

So the output of this step is the list of software tools and components that makeup the system. In other words the *Tech Stack* that someone would ahve to know in order to work on that system.

Note that it may not be necessary to use every component in the entire tech stack for the whole project. The distinguishing question between the two cases is probably: if the user never learns this, does the goal still work?

Output: tech Stack List

## Step 2. Assessment of the User's knowledge base

Once the Tech Stack has been established, it's time to see how well the user knows it.  At this point, the AI should ask the user questions that determine how well the user knows what something does.  This could be any series of questions ranging from "what does this code do?" and showing a snippet or "Write a fucntion in Java that does ____" or it could even involve "What's the derivative of $x^2$ in terms of $x$.  The questions are entirely at the discretion of the AI, as long as they determine how well the user knows the system.  The AI may ask any number of questions, and these question should not feel like the user is getting "tested" or "grilled" but more like "here, let's see what you know so that I can help fill in the blanks for you". 

Output: List of what the user knows about each component of the tech stack and what they don't.

## Step 3. The Search

The AI then goes out and does research on each software component. The research process will consist of at least the following

- Reading the online documentation on the component. 
- Reading the Forums or articles on the the component.
- Reading source code for the component, if available.  

The research process will likely be recursive. eg: in order to know PostGres, you need to know SQL.  So the AI can stop the research once they've reached something the user knows.

output: List of all the pertinant documentation to the tech stack, relative to the user's knowledge base. 

## Step 4. Forming the List

The final step is to form a curriculum of what the user has to do in order to learn each software component and in what order.  There's a certain complexity here. The AI needs to 

- Take the information that has been gathered. 
- Take the user's knowledge about each software component.  
- Cross reference each of the and establish what the user needs to do 
    - What parts of the documentation do they need to read?
    - Waht tutorials will help them learn?
    - After the reading and tutorials, how can they **immediately** apply their newly found skills to the problem that they originally faced.  

For Example, a learning plan might look something like this:

1. Read PostGres Chapter 1.
1. Performt eh Postgres tutorial included in Chapter 1.
    - Apply what you learned to line __ in file ___.py in order to apply this to your problem.
1. Read Postgres Chapter 4. 
    - Apply wat you learned to the application in order to fix _____ bug.  

And it continues from there until everything the user would need to know is stacked into a curriculum they can follow.  

Note that there could be steps in the learning taht are skipped if the user already knows them.

The ordering has to respect prerequisite structure, not just be freeform,so that the user can follow the curriculum exactly. 

Output: The curriculum for the user to follow. 

## Iteration Process

The *Step 2. Assessment of the User's knowledge base*  and *Step 3. The Search* could potentially iterate back and forth if the research uncovers something that needs to be assessed against the user's knowlege.  

There are a couple of possibilities that could happen as the research acrries on through these iterations. 

The stopping side: at some point a node's depth exceeds what's actually load-bearing for the goal. You don't need to understand how the C compiler translates to assembly to write C, you just need to trust it works. So there needs to be a "this is now infrastructure you can treat as a black box" threshold, probably tied back to the relevance filter from way earlier, is this concept required to achieve the goal, or just required to fully understand the tool you're using to achieve the goal. Those are different, and only the first one belongs in the curriculum.

The expansion side: a node turns out to have a prerequisite that's actually necessary, not just interesting, and skipping it would mean the person hits a wall later that the curriculum should have prevented. This is the case where the loop between assessment and search genuinely needs to add a new node to the map rather than close one out.


