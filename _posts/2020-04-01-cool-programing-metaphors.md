---
title: "Cool programing metaphors"
date: 2020-04-01 +0200
categories: decorator strategy brokertopology
---

While reading books or blogs about programing it happens that I encounter such cool explanations or metaphors about a specific topics that I imagine stopping the time and memorizing them on the spot. Since that is not possible, noting them down in a blog post seems like a decent idea.

## Design Patterns

#### Decorator vs Strategy

While comparing `Decorator` and `Strategy` patterns the [GoF](http://wiki.c2.com/?GangOfFour) guys make the a note that the difference between them is like *changing the skin of an object versus changing its guts*:
> We can think of a decorator as a skin over an object that changes its behavior. An alternative is to change the object's guts. The Strategy pattern is a good example of a pattern changing the guts.

<small>pag. 179 - [Design Patterns: Elements of Reusable Object-Oriented Software](https://www.amazon.com/Design-Patterns-Object-Oriented-Addison-Wesley-Professional-ebook/dp/B000SEIBB8) (Erich Gamma, John Vlissides, Richard Helm, Ralph Johnson)</small>

## Architecture

#### Event Driven Architecture - Broker Topology

The event-driven architecture pattern consists of two main topologies, the mediator and the broker. While explaining the broker, [Mark Richards](https://www.goodreads.com/author/show/19751098.Mark_Richards) makes the following analogy:
> The best way to understand the broker topology is to think about it as a relay race. In a relay race, runners hold a baton and run for a certain distance, then hand off the baton to the next runner, and so on down the chain until the last runner crosses the finish line. In relay races, once a runner hands off the baton, she is done with the race. This is also true with the broker topology: once an event processor hands off the event, it is no longer involved with the processing of that specific event.

<small>pag. 17 - [Software Architecture Patterns](https://www.goodreads.com/en/book/show/25091671) (Mark Richards)</small>