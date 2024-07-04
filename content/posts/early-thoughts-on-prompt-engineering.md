---
title: "Early Thoughts on Prompt Engineering"
date: 2024-07-04T20:00:00+00:00
draft: true
---

My initial reaction to the term *prompt engineering* was skepticism that anything of the sort could be called engineering. Having now spent a bit of time using LLM AI to produce a solution to a small content generation problem, I've arrived at a few takeaways, some of which have pushed me to be less dismissive of this notion.

<!--more-->

## Domain knowledge and understanding

Deriving an LLM-based strategy for your problem requires a thorough understanding of the domain and the ability to define a sound mental model of it. You will, after all, be naming things and giving instructions. These should be precise and unambiguous. To skimp on discipline here exposes you to the vagaries of the token generation. The LLM has a universe of knowledge available to it, which &mdash; for all its benefits &mdash; primes it to wander astray of your intended path. Having a clear mental model of the problem, including the parts of it that don't need solving, will help keep you (and it) on track.

Interestingly, good naming in software engineering is mostly just a benefit to humans; in prompt engineering, perhaps it could be likened to algorithmic bedrock.

## Problem decomposition

The principles of sound engineering apply. Breaking the problem down into simpler subproblems seems to yield better results, likely by forcing you to state your intermediate requirements more concretely. The payoff of this effort is driven from the bottom upwards: LLMs are simply more likely to fulfill your request if given less to do and less to consider.

This subproblem definition step is especially important in problem domains where some human expertise already exists, but the implementation details are perhaps mysterious to anyone who isn’t the expert. The success of the solution hinges on this expert being able to express their intuitive grasp of the domain clearly in natural language. Perhaps they even lack that ability, in which case it becomes a task of the prompt engineer and expert to work together to unpack the complexity.

## Modules, Interfaces, Workflows

What follows naturally from defining subproblems is the process of building independent modules of work that can be composed together, ideally by defining interfaces at their boundaries. Any LLM that can be instructed to produce JSON provides this capability. Working with interfaces allows code modules and prompt modules to be interleaved with each other and chained together into workflows and pipelines.

Even if just working with prompts in the absence of code, mapping out the "business" rules &mdash; including the parameters, the conditions upon which to fork logical pathways, the pathways not worth pursuing, etc. &mdash; will produce a series of prompts that encode the decision-making steps, their inputs, and their outputs, i.e. a form of the so-called "giving the model time to think" strategy.

## Framing

This is less of an engineering parallel, but it helps to think of any current, consumer-level LLM as a human agent, with basic reasoning abilities and judgment, that is quite good at interpreting meaning and making associations, but that lacks context and is perhaps weak in raw computation and multi-tasking. It will accomplish what you ask of it insofar as you have presented it with a clearly defined problem in a somewhat known context.

However, it is also blindly subservient, meaning that it will do whatever you ask it to, no matter what, even if that turns out to be the wrong thing to do.
