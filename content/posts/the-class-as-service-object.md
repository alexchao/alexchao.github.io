---
title: "The Class as a Service Object"
date: 2023-05-12T15:54:56-07:00
draft: true
---

One of the things that seems to confirm itself over and over again in my experience as a software engineer is the danger of using classical object-oriented inheritance to share code. In my own experience, I struggle to recall a time when I used inheritance with great success as the core, behavior-sharing construct in an implementation of something. At the very least, of all those moments where I found something resembling an elegant solution, most of the time it was some other pattern that came to the rescue.

This is not a novel observation. I particularly like Brandon Rhodes's expression of this principle in his Python rendition of the [Gang of Four principle, Composition Over Inheritance](https://python-patterns.guide/gang-of-four/composition-over-inheritance/).

Also, this observation is actually a digression from what I want to talk about here, but it is relevant in that it begs one to ask, "What good are classes for?"

# The Class as a Container for Logic

In any software project that grows to a certain size, we inevitably find ourselves having to manage the growing complexity of the system and explosion of business logic. A project often starts out with business logic baked into whatever layer sits closest to the client interface (e.g. the controller in a typical MVC architecture), but as that becomes unwieldy, we look to find a new home for all of this code. Extracting this logic to a new place inherently means taking some lines of code and removing them from the body of a named controller or handler module. Where do these lines of code go then?

The pattern that I see most often and that I like very much is the use of the class to encapsulate a single, well defined unit of work.

{{< highlight ts >}}
class CreateUser {
  private User: UserModel

  constructor(User: UserModel) {
    this.User = User
  }
  
  public async call(attrs: UserAttrs): Promise<UserRecord> {
    const newUser = new this.User(attrs)
    await newUser.save()
    return newUser
  }
}
{{< /highlight >}}

This example is maybe contrived and overly simple, but we can already appreciate a couple things that using a class affords us:

- A name
- Encapsulation
- Separation of dependencies from arguments

Other things:

- Lends itself to compose method pattern
- Exposes an interface, good for testing

[comment]: <> (Code to an interface; not an implementation. Show example where UserModel is an interface instead.)
