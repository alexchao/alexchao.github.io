---
title: 'When to Write Code Comments'
date: Tue, 17 Aug 2021 04:44:44 +0000
draft: false
tags: []
---

Generally speaking, my advice on this topic would be:

> Don't write comments to describe what the code is doing.

Code written in an imperative way can be read line by line to determine what processing is being performed. Re-stating the logic or steps of execution in a comment runs the risk of the comment falling out of sync with the code and becoming outdated.

If a section of imperative code gets big, unwieldy, and hard to read, that's probably a sign that a refactoring is needed and some abstractions need to be introduced. Code written in a declarative way should — in theory — be even more self-explanatory, unless the naming is poor or the wrong abstractions are being used.

There are of course some situations where comments are useful.

### To inform the reader of things that cannot be discerned from reading the code

Sometimes, we have to call functions with funny arguments, or format data in funny ways that defy expectation. Maybe there's some odd side-effect of the function we're calling that forced us to structure the arguments in a strange way, and this workaround was the best option available at the time.

A comment here can dispel some confusion for a newcomer to this area of the codebase (or even for one's future self).

### To describe how a thing should be used

Code alone may not always fully convey how to use a class, function, or module. While unit tests often demonstrate usage effectively, there are cases where a docstring or inline comment can provide duly needed context, such as clarifying the purpose of parameters or raising awareness about specific edge cases. These annotations bridge the gap when even the most clever naming doesn't telegraph the design-thinking behind the code or the circumstantial pressures that led to the implementation.