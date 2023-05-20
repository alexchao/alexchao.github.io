---
title: "The Class as a Service Object"
date: 2023-05-12T15:54:56-07:00
draft: true
---

One thing that repeatedly confirms itself in my experience as a software engineer is the danger of using classical object-oriented inheritance to share code. I struggle to recall a time when I used inheritance with great success as the core, behavior-sharing construct in an implementation of something. At the very least, of all those moments where I found something resembling an elegant solution, most of the time it was some other pattern that came to the rescue.

This is not a novel observation. I particularly like Brandon Rhodes's expression of this principle in his Python rendition of the [Gang of Four principle, Composition Over Inheritance](https://python-patterns.guide/gang-of-four/composition-over-inheritance/).

Also, this observation is actually a digression from what I want to talk about here, but it is relevant in that it begs one to ask, "What good are classes for?"

## The Class as a Container for Stateless Logic

In any software project that grows to a certain size, we inevitably find ourselves having to manage the growing complexity of the system and explosion of business logic. A project often starts out with business logic baked into whatever layer sits closest to the client interface (e.g. the controller in a typical MVC architecture), but as that becomes unwieldy, we look to find a new home for all of this code. Extracting this logic to a new place inherently means taking some lines of code and removing them from the body of a named controller or handler module. Where do these lines of code go then?

The pattern that I see most often and that I like very much is the use of the class to encapsulate a single, well defined unit of work.

{{< highlight ts >}}
class TeaPot {
  public brew(leaves: TeaLeaves, water: Water): Tea {
    // ...
  }
}
{{< /highlight >}}

I've seen these entities referred to with names such as services, service objects, logic components, and logic modules. Whatever the name, they are built to be:

- Small
- Modular and composable
- Reusable

[comment]: <> (Stateless...)

## Benefits

The above example is perhaps contrived and overly simple, but we can already appreciate a few things that using a class affords us.

### A name

We can use the name of the class to denote its function and responsibility.

We're used to seeing class names that take the [agent noun](https://en.wikipedia.org/wiki/Agent_noun) form, like `*Builder` or `*Sender`, but in practice, I've seen classes named in a way that simply states what they do, using a verb phrase or predicate. This obviously deviates from the usual OOP naming conventions, but I don't think that matters too much; we just want to know what the thing does.

"But... functions also have a name..." one might say. More on this a bit later.

### Encapsulation

Classes provide encapsulation to hide data and implementation details, and only expose behaviors through an interface. These are good things; not much more needs to be said about this instrinsic property of classes.

### Separation of dependencies from parameters

This is one I particularly like. Classes have the convenient property of taking "inputs" twice in the course of their normal usage: once during instantiation, and then again when public methods are invoked. It's really up to you as the author to decide how these entrypoints should be used, but the separation between them allows you to signal the different semantics of the things you pass in.

The constructor is a natural place to inject dependencies, as if to say, "These are the things this class needs to get its work done." If we think about the class as a specification for something that performs jobs, the constructor specifies what modules are required to do the job, before a specific job request even arrives. Likely, these modules are also the things that are reusable across multiple job requests (a database connection, an API client, etc.).

[comment]: <> (Class methods as convenience factories.)

### A class lends itself nicely to the Compose Method pattern

It's seemingly such a simple concept that one might hesitate to even call it a design pattern, but the **compose method** pattern involves breaking down program code into small, named, intention-revealing steps, all at roughly the same level of detail. It is so fundamental a pattern that we apply it without being aware of it, and yet there are times when we forget to use it.

The book _Refactoring to Patterns_ by Joshua Kerievsky contains this figure, which I think illustrates the concept in Java pretty well, using a self-expanding list type as an example:

#### Before refactoring...

{{< highlight java >}}
public void add(Object element) {
  if (!readOnly) {
    int newSize = size + 1;
    if (newSize > elements.length) {
      Object[] newElements = new Object[elements.length + GROW_SIZE];
      for (int i = 0; i < size; i++)
        newElements[i] = elements[i];
      elements = newElements;
    }
    elements[size++] = element;
  }
}
{{< /highlight >}}

#### After refactoring...

{{< highlight java >}}
public void add(Object element) {
  if (readOnly)
    return;
  if (atCapacity())
    grow();
  addElement(element);
}
{{< /highlight >}}

Using private methods of a class to encapsulate subdivided units of work makes it a very natural process to repeatedly perform [extract method](https://refactoring.com/catalog/extractFunction.html) on the more gnarly blocks of your code. The class itself effectively serves a grouping namespace for the related bits of logic, keeping things nice and tidy. Additionally, if the language supports access modifiers (`public`, `private`, etc.), you can explicitly communicate the intended availability of each piece of logic to other developers.

### An interface, with all its attendant benefits

A well-thought-out class will implement an interface, but even with no predetermined interface, one can be derived after the fact. Simply having an interface enables a range of benefits owing to the age-old principle:

> Program to an interface, not an implementation.

One of these benefits is flexibility in testing.

In a system where many such service objects exist to handle application logic, complex tasks will be performed by many service objects that compose and depend on each other. Designing logic to depend on the _interface_ of a downstream service object, rather than directly on the service object itself, makes it possible to substitute mocks and stubs in for the real thing.

Here's an implementation of a class that depends directly on the types of its dependencies:

#### The class definition itself...

{{< highlight ts >}}
class BobaClerk {
  private teaPot: TeaPot
  private integredientStore: IngredientStore
  private kitchen: Kitchen

  constructor(teaPot: TeaPot, integredientStore: IngredientStore, kitchen: Kitchen) {
    this.teaPot = teaPot
    this.integredientStore = IngredientStore
    this.kitchen = kitchen
  }
  
  public makeBoba(order: Order): CupOfBoba {
    const {
      teaLeaves,
      toppings,
    } = this.integredientStore.getIngredients(order)

    const water = this.kitchen.getWater()
    const tea = this.teaPot.brew(teaLeaves, water)
    return new CupOfBoba(tea, toppings)
  }
}
{{< /highlight >}}

#### And it's accompanying test

{{< highlight ts >}}
describe('BobaClerk', function () {
  it('makes a cup of boba' function () {
    const teaPot = new TeaPot()
    const ingredientStore = new IngredientStore()
    const kitchen = new Kitchen()

    const bobaClerk = new BobaClerk(teaPot, ingredientStore, kitchen)

    const order = new Order({
      teaType: TeaType.oolong,
      toppings: [Topping.mangoBoba, Topping.nataDeCoco],
    })

    const cupOfBoba = bobaClerk.makeBoba(order)

    expect(cupOfBoba.flavorProfile()).to.equal({
      roastLevel: 'medium-light',
      mouthfeel: 'chewy',
    })
  })
})
{{< /highlight >}}

Seemingly simple enough. This test lacks an expectation about the sending of the welcome email, but finding a way to mock the `sendNewUserWelcome` method of the `EmailService` class should not be difficult.

Still, needing to create an instance of `EmailService` could serve as a possible annoyance, especially in a more complex example where it has a myriad of dependencies and possible side effects (indeed, one would expect a module called `EmailService` to at least make some network calls).

And to return to the point about mocking the `sendNewUserWelcome` method: a mock or stub here would have to mean the `sendNewUserWelcome` method name appearing somewhere in this test file (presumably, you would have some line of code like: `mock(emailService).expects('sendNewUserWelcome').once().withArgs(...)`).

Now, the same implementation 

## Trade-offs

### Verbosity

Most of what I like about this pattern

### Anemic Model

### Performance

Object instantiation invariably has a cost, and the cost probably differs from language to language. In a context where your code is being executed rapidly with a high number of iterations, the expressive benefits of the class structure probably won't outweigh the performance costs.
