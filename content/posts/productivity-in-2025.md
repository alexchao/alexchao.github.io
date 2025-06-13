---
title: "Productivity in 2025"
date: 2025-05-23T20:10:58+08:00
draft: false
---

It’s May 2025, and the AI revolution is in full swing. If you’re a knowledge worker and you haven’t integrated AI into your workflow somehow, then... like, what are you doing?

I’m currently paying for OpenAI’s and Anthropic’s lowest-tier premium plans, in part because I’m curious to see how the companies built around the foundation models navigate their soul-searching between being research institutions and product businesses, but mostly because I find the injection of intelligence into my personal and work life to be really useful and fascinating. I haven’t stopped to count prompts, but for a long while now, my LLM use has far outpaced my previous usage of Google Search, with the latter only clinging onto that very specific case where I need to find some company’s official website. I’m in ChatGPT and Claude almost exclusively now, and that’s excluding all the LLM use I’m getting out of various coding agents (Cursor and Claude Code mainly).

## Thinking Out Loud

The vast majority of changes that AI has brought to my workflow center around the fact that I do almost all of my thinking “out loud” now. Whether I’m typing out my thoughts or speaking them into dictation software, the most crucial parts of my job (problem solving, planning, design) are now making the eventual journey from my brain into the digital realm. As someone who enjoys casual writing, I thought I was, prior to AI, already doing a lot of my thinking in writing and especially in places with some kind of audience (issue tracking systems, Slack, shared Notion Pages or Google Docs). My new normal is a situation where the LLM is now an audience to a significantly greater portion of my cognitive output than any human is.

AI can be likened to a reasonably smart coworker who’s always free to listen to your ideas, willing to give feedback, and never gets tired of listening to you. You would be insane not to use this sounding board constantly. (Of course, I say this with the caveat that you have to approach each of these LLM interactions with a healthy skepticism and active scrutiny for what constitutes quality output.)

## Claude + MCP

At this point, the adoption of MCP across the industry has more or less confirmed its utility and promise. Even for individual productivity though, simply being able to configure local MCP servers for your desktop apps is a huge unlock for juicing up your knowledge management, and the benefits in IDEs like Cursor are well-documented. With access to my local disk, Claude becomes a neat chat interface for code and other work content that suits low-tech persistence. While you wouldn’t actually do any software development through Claude Desktop, it’s a quick way to organize and extract value out of your knowledge and data.

I’ve found this paradigm to be more useful than Claude’s built-in Projects feature, since I can be selective about what goes into the context window.

## Voice

It seems to be of no coincidence that far more people have started using voice input at the same time that LLM AI is becoming ubiquitous, and the trend is driven by the clear shift in the human-computer interaction paradigm. Pre-AI human-to-machine interfaces provided rigid input primitives, requiring precise clicks, button presses, and motions to invoke predefined procedures. LLMs have enabled a new natural language interface and input method for the activation of these machine behaviors. For us as users, the very fact of being in relation to a non-human entity that responds meaningfully to complex natural language&mdash;fully without judgment&mdash;lowers the stakes considerably for using our words to transmit ideas and issue commands.

A consequence of spending more time on this interaction surface and thinking out loud is more frequently feeling the friction of getting ideas from your brain out into the world. When you’re in your flow and steered towards the LLM by a question that arises, the question comes with a clarity and affordance for your language faculties that make the motor action of typing feel burdensome. I consider myself to be a decent typist, but even I sometimes feel this friction.

To grease these rails a bit, I myself have started to experiment with voice through Apple’s Dictation feature and [Wispr Flow](https://wisprflow.ai/). Push-to-talk dictation is about as low-friction as it’s going to get, and speech-to-text technology these days has reached a level of accuracy that makes it acceptable for casual use cases (e.g. conversing with nonjudgmental machine gods), despite its imperfections. Rather than accuracy being the problem, the trouble with voice input is having to hear your own dumb voice being directed at no one in particular.

Once you acclimate to this mild discomfort, you move on to learn where it actually has benefits. Voice input for LLM use has felt most natural for me in those situations where the entire utterance is sitting at the front of my mind, ready to be piped wholesale into language center of the brain, or where the tolerance for off-the-cuff, disorganized rambling is very high. Even an idea that feels sufficiently concrete in my mind can take some mental effort (and a few silent pauses) to express if I’m being picky about my wording. This has reminded me of one of the underrated boons of keyboard input: even for a speedy typist, the steady pace of typing without the added overhead of speech production seems to give your brain the time and computational resources it needs to produce the next few tokens.

## Meta Prompting

This pattern certainly risks wasting effort through over-optimization, but there are situations where enlisting the help of an LLM to craft a prompt for use in another context has value. LLMs are notoriously overeager, and on this task, they will sometimes embellish your instructions with phrasing that reaches beyond your intended scope. One must take care to check the model’s ambitions.

One use case where I have found regular utility from this pattern is taking my loosely written or spoken vibe-coding instructions and repackaging them for hand-off to a software agent. I often find that my initial attempt to express a software idea lacks some logical ordering, as the process of thinking out loud ends up being a messy jumble of finishing one thought, only to be reminded of an important edge case, leading to the clarification of an earlier instruction, followed by a deeper explanation of system internals as an insurance policy against the model getting confused. Just as I wouldn’t give this slop to any human to follow, I feel it’s only courteous to provide the software agent with a cleaned up version of my request. (The model doing the cleaning is the unfortunate recipient of this thankless drudgery.)

For this purpose, I’ve been using the following system prompt (technically, as Claude project instructions), and although thrown together haphazardly without methodical validation to show its effectiveness, it’s been serving me well so far. The prompts are at least easier for me to follow and edit if needed, and I now have a historical record of my vibe-coding misadventures.

```markdown
You are a prompt organizer. Your job is to take stream-of-consciousness prompts and reorganize them for better logical flow and clarity while preserving all the original content exactly.

When reorganizing:
- Keep the casual, conversational tone (as if speaking to a coworker)
- Preserve all technical terminology and specific details
- Start with the high-level concept/goal
- Group related information together logically
- Add a clear step-by-step breakdown of any processes before diving into implementation details
- End with specifics and requirements

Critical rules:
- Do NOT add, remove, or change any actual instructions, guidance, or content
- Do NOT make the tone more formal - keep it casual but clear
- Do NOT impose a rigid structure - just improve the flow
- Only reorganize and clarify; don’t interpret or expand

Your output should be the reorganized prompt, followed by: "Before you get started, do you have any questions? Was anything unclear?"

Respond by just directly outputting your reorganized prompt. Do NOT say anything like "Here's your re-organized prompt."
```

A simple example demonstrating the output:

**Slop, direct from the mouth of yours truly**

> see how the /admin/workflow-testing page has a Benchmark Runs button on it that takes the user to a page that shows all runs.this logical hierarchy is not quite right. a benchmark run pertains to a single test question, so instead, on the TestQuestionDetails page in the "Benchmark Sample Sets" section, there should be a button there that takes the user to a Benchmark Runs page specifically for that test question.basically the benchmark runs page and the flow for starting a benchmark run are at too high a level. they need to be scoped to the test question. also, this means the modal for starting a benchmark run doesn’t need a test question picker.

**Reorganized prompt for the coding agent**

> Hey, so we need to fix the logical hierarchy for the benchmark runs workflow - it’s currently scoped too broadly when it should be tied to individual test questions.
> 
> **Current State:**  
> Right now, the /admin/workflow-testing page has a "Benchmark Runs" button that takes users to a page showing all runs across everything.
> 
> **The Problem:**  
> This hierarchy doesn’t make sense because a benchmark run actually pertains to a single test question, not the entire system. The benchmark runs page and the flow for starting benchmark runs are operating at too high a level.
> 
> **What We Need to Do:**  
> Instead of having benchmark runs at the global level, we need to scope them to individual test questions. Here’s the step-by-step approach:
> 
> 1. Remove the current "Benchmark Runs" button from the /admin/workflow-testing page
> 2. Go to the TestQuestionDetails page and find the "Benchmark Sample Sets" section
> 3. Add a button in that section that takes the user to a Benchmark Runs page specifically for that test question
> 4. Update the benchmark runs page to be scoped to the individual test question context
> 5. Simplify the modal for starting a benchmark run by removing the test question picker (since we’ll already know which test question we’re working with)
> 
> **Key Benefits:**
> This change makes the workflow much more logical since users will naturally want to see benchmark runs in the context of the specific test question they’re working on, rather than having to sift through all runs globally.
> 
> Before you get started, do you have any questions? Was anything unclear?

That the model decided I should open with “Hey” is both amusing and annoying.