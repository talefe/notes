# 1.1. Principles of OOP programming!

## 1.2. The 4 pillars of OOP

These are:

-   Abstraction
-   Encapsulation
-   Inheritance
-   Polymorphism

&nbsp;

## 1.3. Abstraction!

![abstraction][abstraction-image]

One of the most important pillars behind OOP.  
Abstraction is defined by IEEE (Institute of Electrical and Electronics Engineers) as

> A view of a problem that extracts the essential information relevant to a particular purpose and
> ignores the remainder of the information

The idea here is that through abstraction, we are unable to simplify a problem or a representation
only to the extent of detail that is needed for the problem at hand.

&nbsp;

In an attempt to pay some homage to the class I got on this from Sérgio:

![not-a-pipe][not-a-pipe-image]

Let's start with: try and answer the question: What is it that you are looking at?  
You might be tempted to go right ahead and answer that it is a pipe. But is it? Even the sentece
itself says otherwise... If it isn't a pipe what is it that you are currently in the presence of?...
After some consideration you will probably then get to the conclusion that what you're seeing is a
painting. Well, you are right. But alas you are wrong as well.

In fact you are looking at a photo of a paiting of a pipe.  
Better yet, if we want to be quite strict about it, you are in fact looking at a bunch of pixels
being light up in a screen, _**representing**_ a photo _**of**_ a painting _**of**_ a pipe.  
And yet, this was plenty enough for all of us involved to know that we are thinking of a pipe,
right?  
Even deeper: the simple mentioning of the word pipe is enough for us to all know what we are talking
about.

The entire concept of a language is based on abstraction. Damn that's some _deep shit_.

Ok but but lets take a step back, understand how we got here, and what this whole idea of
abstraction means to programming.  
As previously stated, the idea is that we abstract only enough of a problem so that we can handle
it.

Say I have a game where a master coder is featured.  
What level of abstraction will I be needing? Well say that I want to have a bored Rolo in my game.

![increasing-abstraction][increasing-abstraction-image]

Well, my abstraction of Rolo doesn't need to involve all the complexity involved in a photo of him,
will it?  
Will it involve the complexity of a (let's pretend) well drawn image of him?... Hmm...

The consideration that I have to go to is what will "Rolo" represent towards my game.  
If we boil it down really hard, what I need to represent Rolo is simply a bearded guy with his messy
hair and some glasses. (And a tiny dark cloud above his head?)

This is the same approach that we should aim at when we're programming. The abstraction is what
allows us to deal with the tremendous complexity that any given entity can have if we try to think
about all the tiny details that actually make it up, by boiling it down to only consider the aspects
that are important to my scenario.

Do you remember car crash? Why didn't you call it "square collider"? You accepted the abstraction
that a colored rectangle in your screen represented a car.

And if that's not pretty amazing, _I don't know what is_.

&nbsp;

## 1.4. Encapsulation?

Encapsulation deals with and allows us to implement as loose coupling as possible between our
objects.  
It's one of the great marvels of OOP, as it is one of the things what gives it it's modularity, that
possibility of swapping components the way we talk so much about. (Yes, coupled with a few more
features...) Good encapsulation allows for software that is both more scalable and easier to
maintain.

As stated in the slide:

> Encapsulation or equivalently information hiding refers to the practice of including within an
> object everything it needs, and furthermore doing this in such a way that no other object need
> ever be aware of this internal structure - Graham, 1991

Despite the exact definitions of `Encapsulation` vs `Information hiding` not perfectly being
interchangeable and there's some discussion that could be had here, let's delve into what we
actually mean in the slides/what matters for the issue at hand.

The idea is that the less each entity knows about the inner workings of any other entity, the less
even we as programmers need to know.  
Encapsulation is the marvel that allows you to make use of a CachedThreadPool without the need to
know how it works on its inside, or even what properties it has.

One interesting rule to mention about the principle of encapsulation is the [Law of
Demeter][law-of-demeter-link] (or more [here][law-of-demeter-wikilink]. Yes I know it's wikipedia
but even `Clean Code` references this page). This law is concerned about what an object's method is
allowed to interact with.  
(Consider when you read `messaging` you can interpret it as `call a method on`. The concept of
messaging derives from the early days of OOP, when the concept was that objects communicated by
sending messages amongst themselves)

> For all classes C, and for all methods M attached to C, all objects to which M sends a message
> must be
>
> -   M’s argument objects, including the self object or
> -   The instance variable objects of C (Object created by M, or by functions or methods which M
>     calls, and objects in global variables are considered as arguments of M.)

Which can be decodified into:

-   For all classes C, and all methods M from class C, all objects to which M sends a message must
    be:
    -   itself (the `this`in Java)
    -   M's argument objects
    -   Instance variable objects of C
    -   Objects created by M, or by functions or methods that M calls
    -   Objects in global variables (`public static` object fields in Java)

If you consider and apply the rules of this law you should be able to get quite the great
implementation of encapsulation.

&nbsp;

## 1.5. Encapsulation vs Abstraction

The concept of _Abstraction_ is what allows us to deal with only what is essential to the system
that we're aiming to implement.

The concept of _Encapsulation_ is what allows us to enclose the inner workings of our entities,
exposing only the functionality that we intend to.

&nbsp;

## 1.6. Object Interface

We consider that the interface of an object is what the functionality that is delivers to the
outside.

Objects in OOP programs communicate with each other through use of those public interfaces.

![object-interface][object-interface-image]

&nbsp;

## 1.7. Aggregation vs Composition

These are two sides of the same coin, that coin being the idea of what we in Java call
composition.  
The idea is that the `HAS-A` relationship that we've by now become familiarized with can be ranked
at two different levels.

One being what we can call specifically "Composition", in which the idea is that the relationship is
so strong that the external class is made up of the classes it "owns", and those can not exist
without the containing class.

The other we call "Aggregation", and the relationship estabilished is not as strong as in the
concept of composition, meaning that the contained class can exist without an instance of the
containing one.

The example in the slides pertains to:

-   A CD contains several Songs and those can't exist (in this example) without an instance of they
    containing class, estabilishing a composition relationship
-   A Car has an Engine but the engine can exist ouside of the car, for example in a boat or
    airplane, meaning that then this is an aggregation relationship, not as strong as the
    composition's one.

Despite this difference, we refer to both quite interchangeably as Composition, and they both
create an `HAS-A` relationship

## 3.1 Architectural patterns

While design patterns are concerned about solving problems at the level of the different
collaborating objects, there are patterns that occur at very different levels.

Patterns occurring at a larger scope and that cover the fundamental organization of a system are
considered Architectural Patterns. They aim to provide reusable solutions to common problems in
structuring software, the same way that design patterns do, except at a different scape.

&nbsp;

## 3.2. Model View Controller

&nbsp;

## 3.3. MVC

The MVC pattern is a very commonly used Architetural Pattern, found in a lot of applications of the
most diverse types. Chances are that the cadets will end up working on an application built either
on this pattern or in one of its variants.  
The general concept this pattern aims to implement is the division of a given software application
into three interconnected layers, thus achieving the separation of the internal representation of
the data from they way that the user interacts with it.

&nbsp;

## 3.4. The pattern's layers' responsabilities

The model:

-   represents the domain data
-   contains the business logic
-   communicates to the persistence mechanism underneath the application

The View:

-   represents the user interface, what the user will actually see
-   is responsible for providing ways to interact with the application

The controller:

-   acts as an intermediary between the model and the view layers
-   is the one responsible for mapping the users's actions and inputs to the execution of those on
    the model's side

&nbsp;

## 3.5. The flow of events

![mvc-flow][mvc-flow-image]

In a MVC implementation, the flow of handling an event will be the following:

1. A user interacts with a view
2. The view will alert a specific controller about the occurrence of the event
3. The controller will then update the model accordingly
4. The model notifies the view that his status has changed
5. the view fetches the model's renewed data and updates itself

&nbsp;

## 3.6. M-V-Whatever

With this explained, there are several variations to the classic MVC pattern. They keep on building
upon the idea of separating the data from the presentation and hiding the logic that interconnects
them behind a controller object.

-   MVP evolved when the applications grew in size and testing became more and more relevant. An
    entity that is the presenter is given total access to a view that generally is very passive and
    will be created declaratively, responding to data binding and no more.

![mvp-flow][mvp-flow-image]

-   MVVM attempts to separate the development of UI's from the aplication behaviour and business
    logic by making sure that the view only has data bindings to the view-model, which allows for
    complete separation of work on view from other layers.

&nbsp;

## 3.7. {Exercise} Apply MVC to JavaBank

&nbsp;

## 3.8. Service Layer Pattern

So, now that we have just implemented the MVC patter to our application, we managed to get some
separation between different parts of our application's logic. But we can go a bit further.

If I decide to encapsulate the business logic of my program, where should I place it?

-   In the model? - This is a common practice but it has a few drawbacks. Your objects will quickly
    become fat with too many responsabilites, and you will end up coupling your models in between
    themselves (For example if you have the concept of a customer and products, where will you now
    place the logic of a customer aqcuiring a product? Either way you decide to do it, you will
    couple one of the models to the other.)
-   In the controller? - This is actually an anti-pattern, as this way you would be handling the UI
    actions, the access to the data and the business logic all in the same layer, which is a
    terrible idea. The buiness logic should be completely separated (and thus protected) from any
    possible changes in the UI. Which are pretty common.

A solution that is cleaner and in fact more scalable it to then extract this business logic into its
own layer, which we will be calling the Service Layer. By using this pattern, the controller becomes
responsible for receiving the request data and passing it onto the service layer, who then performs
actions upon the necessary models and returns data for the controller to inject into a View again.

## 3.9. Service interface

A slide with a few examples of Service layer interfaces

## 3.10. {Exercise} Apply a service layer to the javabank app

[//]: # 'LINKS TO VARIOUS EXTERNAL RESOURCES'
[law-of-demeter-link]: https://dzone.com/articles/the-genius-of-the-law-of-demeter
[law-of-demeter-wikilink]: https://en.wikipedia.org/wiki/Law_of_Demeter
[//]: # 'LINKS TO IMAGES AND SIMILAR RESOURCES'
[mvc-flow-image]: resources/images/mvc-flow-drawing.jpeg
[mvp-flow-image]: resources/images/mvp-flow-drawing.jpg
[abstraction-image]: resources/images/abstraction.png
[not-a-pipe-image]: resources/images/not-a-pipe.jpg
[increasing-abstraction-image]: resources/images/increasing-abstraction.jpg
[object-interface-image]: resources/images/object-interface.jpg
