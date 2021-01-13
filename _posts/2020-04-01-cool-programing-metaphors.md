---
title: "Cool programing metaphors"
date: 2020-04-01 +0200
last_modified_at: 2020-07-16 +0200
categories: stack brokertopology decorator strategy garbagecollection domaindrivendesign entity valueobject
toc: true
toc_label: Topics
toc_icon: quote-right
---

While reading books or blogs about programing it happens that I encounter such cool explanations or metaphors about a specific topics that I imagine stopping the time and memorizing them on the spot. Since that is not possible, noting them down in a blog post seems like a decent idea.

## Fundamentals

### Collections

#### The Stack

Also known as LIFO (Last In First Out) the Stack is just another collection with few restrictions. It is described with humor by [Rob Conery](https://rob.conery.io/) like this:

> The simplest way to think about the stack is by visualizing one of my big pet peeves: a stack of plates. The ones on the bottom never get used because we always grab the plates on the top!

![image-center](/assets/images/imp-handbook-the-stack.png){: .align-center}

<small>pag. 152 - [The Imposter's Handbook](https://bigmachine.io/products/the-imposters-handbook/) (Rob Conery)</small>

## Architecture

### Event Driven Architecture - Broker Topology

The event-driven architecture pattern consists of two main topologies, the mediator and the broker. While explaining the broker, [Mark Richards](https://www.goodreads.com/author/show/19751098.Mark_Richards) makes the following analogy:
> The best way to understand the broker topology is to think about it as a relay race. In a relay race, runners hold a baton and run for a certain distance, then hand off the baton to the next runner, and so on down the chain until the last runner crosses the finish line. In relay races, once a runner hands off the baton, she is done with the race. This is also true with the broker topology: once an event processor hands off the event, it is no longer involved with the processing of that specific event.

<small>pag. 17 - [Software Architecture Patterns](https://www.goodreads.com/en/book/show/25091671) (Mark Richards)</small>

### Domain Driven Design

#### Entities

In domain driven design a model expressed in software follows usually one of the three model paterns: `ENTITIES`, `VALUE OBJECTS` and `SERVICES`. We say an object is an `ENTITY` when it is distinguished by its identity, rather than its attributes. [Eric Evans](https://domainlanguage.com/tag/eric-evans/)'s stadium analogy explains it better:

> An application for booking seats in a stadium might treat seats and attendees as ENTITIES. In the case of assigned seating, in which each ticket has a seat-number on it, the seat is an ENTITY. Its identifier is the seat number, which is unique within the stadium. The seat may have many other attributes, such as its location, whether the view is obstructed, and the price, but only the seat number, or a unique row and position, is used to identify and distinguish seats.

> On the other hand, if the event is “general admission”, meaning ticket-holders sit wherever they find an empty seat, there is no need to distinguish individual seats. Only the total number of seats is important. Although the seat numbers are still engraved on the physical seats, there is no need for the software to track them, and, in fact, it would be an error in the model to associate specific seat numbers with tickets, since there is no such constraint at the event. Then seats are not ENTITIES, and no identifier is needed.

<small>pag. 67 - [Domain-Driven Design - Tackling Complexity in the Heart of Software](https://www.goodreads.com/book/show/179133.Domain_Driven_Design) (Eric Evans)</small>

#### Value Objects

On the other hand the same Eric Evans explains `VALUE OBJECTS` as objects that have no conceptual identity and which describe some characteristic of a thing:

> If a child is drawing, he cares about the color of the marker he chooses. He may care about the sharpness of the tip. But if there are two markers of the same color and shape, he won’t care which he uses. If a marker is lost and replaced by another of the same color from a new pack, he can resume his work unconcerned about the switch. 

> Ask the child about the various drawings on the refrigerator and he will quickly distinguish those he made from those his sister made. He and his sister have useful identities, as do their complete drawings. But imagine how complicated it would be if he had to track which lines in a drawing were made by each marker. Drawing would no longer be child’s play.

<small>pag. 70 - [Domain-Driven Design - Tackling Complexity in the Heart of Software](https://www.goodreads.com/book/show/179133.Domain_Driven_Design) (Eric Evans)</small>

## Design Patterns

### Decorator vs Strategy

While comparing `Decorator` and `Strategy` patterns the [GoF](http://wiki.c2.com/?GangOfFour) guys make the a note that the difference between them is like *changing the skin of an object versus changing its guts*:
> We can think of a decorator as a skin over an object that changes its behavior. An alternative is to change the object's guts. The Strategy pattern is a good example of a pattern changing the guts.

<small>pag. 179 - [Design Patterns: Elements of Reusable Object-Oriented Software](https://www.amazon.com/Design-Patterns-Object-Oriented-Addison-Wesley-Professional-ebook/dp/B000SEIBB8) (Erich Gamma, John Vlissides, Richard Helm, Ralph Johnson)</small>

## .NET Internals

### Garbage Collection

Garbage Collection timing is a delicate matter and I found to be perfectly explained by [Maoni Stephens](https://devblogs.microsoft.com/dotnet/author/maoni/) in his Food Court analogy:

> If you observe at a food court, in order to be productive, the janitor tries to collect a sizable amount of dirty dishes when they come out to collect, which means they collect more often when it’s busy to not risk running out of clean dishes, and less often when it’s not busy because there are very few dishes to be collected. This is the same way that the GC tunes. The dirty dishes are like the space occupied by dead objects – it was used (ie, dirtied) and can now be reclaimed. The clean dishes are like the cleared space GC hands out for people to use for new objects, ie, allocations. If GC does a collection and didn’t find much dead space, meaning high survival rate, it will wait till more cleared space is used, or in other words, more allocations are made before it does the next collection.

> During meal times, food courts are busy so the clean dishes are consumed more quickly, and the janitor adjusts to that. This is the same as GC adjusts the amount of allocations before the next collection. It’s called the allocation budget. And this “adjusting” that GC does is part of its dynamic tuning. As the process runs, GC will modify this allocation budget according to the survival rate it observes to keep itself productive.

> Now, the janitor needs a way to recognize if a dish is still in use – it would be quite rude for the janitor to take your dish away if you are still in the middle of using it (if they do that a lot I imagine they’d be fired…). If you are still eating, that’s pretty obvious. That’s the most common scenario. If say you need to leave temporarily (like if you suddenly remembered you needed to get a slice of cake before that dessert place closes…), you might put your jacket on the chair to indicate that you are still here. GC also needs to know if an object is still in use. The most common way is just by one object having a reference to another and that’s obvious to the GC. And there also exist other less common ways that require more effort to indicate to the GC that an object is in use, for example, the GC handles.

<small>[Garbage Collection at Food Courts](https://devblogs.microsoft.com/dotnet/garbage-collection-at-food-courts/) (Maoni Stephens)</small>