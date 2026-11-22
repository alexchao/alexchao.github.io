---
title: "Building with AI"
date: 2026-10-16T16:54:05-07:00
draft: false
---
For a little over 6 months now, I’ve been working in a fairly entrenched AI engineering role. The job looks nothing like the work I had been doing for most of my career as a software engineer, and yet the degree of change still managed to sneak up on me in such a way that I never once felt like I was being thrown into the deep end of something completely new. Every month just brought with it a new normal that was slightly different, slightly more AI-driven than the month before.

Every now and then I catch myself reflecting on how the nature of work as an engineer and builder has changed. It’s probably true in principle that the core elements actually haven’t changed that much, and that problem solving and figuring out what to build under the constraints you’re given is still at the heart of what we do, but it’s impossible not to notice what shifted in the content of my day-to-day work. Coding in English has pushed the mechanics of all the tools I used to use (git, bash, cli tools) to the periphery of my work mind, and I’m almost certainly losing any muscle memory I had in vim.

Now, we manage agents and no longer perform any low-level implementation work. We strive to parallelize our work as much as possible, fanning out our tasks and half-baked ideas across several agents at a time. The resulting volume of work and never-ending cascade of agents exiting their loop and waiting for human input requires a degree of context-switching that was never asked of us when we were still writing code in long stretches of focus. Coming away from a full day of coding used to leave one fatigued in a way that could be described as having nothing left in the tank. Now I get to the end of a day and my mind is in a dizzying haze from constantly thrashing across multiple workstreams.

The experience of frequently forgetting what I’m doing in a particular Claude Code session has led me to think that coding agents should principally allow a builder to go faster and deeper in their existing scope, rather than aggressively expanding their scope into other areas. The limiting factor seems to be the number of mental models one has to sustain: insofar as I, the human, hold all the context and am the authority on what the problem is and what solving it looks like, the scope that I am responsible for is constrained by my ability to maintain clarity on the relevant mental models, especially how they change over time.

Building effectively amounts to solving the tooling and process problems to get that context out of one’s head and into agent-accessible artifacts: evals, specs, examples, etc. This mostly amounts to breaking down walls and barriers to data, unifying system data with the messy ocean of all the stuff that gets said in a multitude of channels between humans and agents working together.

I don’t think a lot about what coding used to be like, but if I recall the memories I have of sitting in front of a traditional IDE, the scale and scope of the problems we used to work on permitted an honesty and intimacy between the programmer and his or her code that I miss.
