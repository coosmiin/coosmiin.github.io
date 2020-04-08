---
title: "Cool programing metaphors"
date: 2020-04-01 +0200
categories: decorator strategy brokertopology
toc: true
toc_sticky: true
---

While reading books or blogs about programing it happens that I encounter such cool explanations or metaphors about a specific topics that I imagine stopping the time and memorizing them on the spot. Since that is not possible, noting them down in a blog post seems like a decent idea.

## Fundamentals

### Collections

#### The Stack

Also known as LIFO (Last In First Out) the Stack is just another collection with few restrictions. It is described with humor by [Rob Conery](https://rob.conery.io/) like this:

> The simplest way to think about the stack is by visualizing one of my big pet peeves: a stack of plates. The ones on the bottom never get used because we always grab the plates on the top!

<figure><img class="image-popup" src="img\imp-handbook-the-stack.png"></img></figure>

## Architecture

#### Event Driven Architecture - Broker Topology

The event-driven architecture pattern consists of two main topologies, the mediator and the broker. While explaining the broker, [Mark Richards](https://www.goodreads.com/author/show/19751098.Mark_Richards) makes the following analogy:
> The best way to understand the broker topology is to think about it as a relay race. In a relay race, runners hold a baton and run for a certain distance, then hand off the baton to the next runner, and so on down the chain until the last runner crosses the finish line. In relay races, once a runner hands off the baton, she is done with the race. This is also true with the broker topology: once an event processor hands off the event, it is no longer involved with the processing of that specific event.

<small>pag. 17 - [Software Architecture Patterns](https://www.goodreads.com/en/book/show/25091671) (Mark Richards)</small>

## Design Patterns

#### Decorator vs Strategy

While comparing `Decorator` and `Strategy` patterns the [GoF](http://wiki.c2.com/?GangOfFour) guys make the a note that the difference between them is like *changing the skin of an object versus changing its guts*:
> We can think of a decorator as a skin over an object that changes its behavior. An alternative is to change the object's guts. The Strategy pattern is a good example of a pattern changing the guts.

<small>pag. 179 - [Design Patterns: Elements of Reusable Object-Oriented Software](https://www.amazon.com/Design-Patterns-Object-Oriented-Addison-Wesley-Professional-ebook/dp/B000SEIBB8) (Erich Gamma, John Vlissides, Richard Helm, Ralph Johnson)</small>

## .NET Internals

#### Garbage Collection

Garbage Collection timing is a delicate matter and I found to be perfectly explained by [Maoni Stephens](https://devblogs.microsoft.com/dotnet/author/maoni/) in his Food Court analogy:

> If you observe at a food court, in order to be productive, the janitor tries to collect a sizable amount of dirty dishes when they come out to collect, which means they collect more often when it’s busy to not risk running out of clean dishes, and less often when it’s not busy because there are very few dishes to be collected. This is the same way that the GC tunes. The dirty dishes are like the space occupied by dead objects – it was used (ie, dirtied) and can now be reclaimed. The clean dishes are like the cleared space GC hands out for people to use for new objects, ie, allocations. If GC does a collection and didn’t find much dead space, meaning high survival rate, it will wait till more cleared space is used, or in other words, more allocations are made before it does the next collection.

> During meal times, food courts are busy so the clean dishes are consumed more quickly, and the janitor adjusts to that. This is the same as GC adjusts the amount of allocations before the next collection. It’s called the allocation budget. And this “adjusting” that GC does is part of its dynamic tuning. As the process runs, GC will modify this allocation budget according to the survival rate it observes to keep itself productive.

> Now, the janitor needs a way to recognize if a dish is still in use – it would be quite rude for the janitor to take your dish away if you are still in the middle of using it (if they do that a lot I imagine they’d be fired…). If you are still eating, that’s pretty obvious. That’s the most common scenario. If say you need to leave temporarily (like if you suddenly remembered you needed to get a slice of cake before that dessert place closes…), you might put your jacket on the chair to indicate that you are still here. GC also needs to know if an object is still in use. The most common way is just by one object having a reference to another and that’s obvious to the GC. And there also exist other less common ways that require more effort to indicate to the GC that an object is in use, for example, the GC handles.

<small>[Garbage Collection at Food Courts](https://devblogs.microsoft.com/dotnet/garbage-collection-at-food-courts/) (Maoni Stephens)</small>