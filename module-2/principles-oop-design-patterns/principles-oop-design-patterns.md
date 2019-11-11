# 1.1. Principles of OOP programming!

## 1.2. The 4 pillars of OOP

These are:

-   Abstraction
-   Encapsulation
-   Inheritance
-   Polymorphism

And we're about to talk about all of them.

&nbsp;

## 1.3. Abstraction!

![abstraction][abstraction-image]

One of the most important pillars behind OOP...

_**Or behind any programming at all!**_

Abstraction is defined by IEEE (Institute of Electrical and Electronics Engineers) as

> A view of a problem that extracts the essential information relevant to a particular purpose and
> ignores the remainder of the information

The idea here is that through abstraction, we are unable to simplify a problem or a representation
only to the extent of detail that is needed for the problem at hand.

&nbsp;

**TL;DR ? from here up until the next slide these are just cool considerations for you to have a
read at if that's your thing ;)  
Feel free to skip ahead**

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
This is also true for the fact that it makes our lifes as programmers easier, since it simplifies
what and how we deal with entities while we're practicing our art.

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

One interesting thing to go read up on is this rule that even Uncle Bob makes a mention of ('Clean
Code' - chapter 6: Objects and Data Structures) about the principle of encapsulation called the [Law
of Demeter][law-of-demeter-link] (or more [here][law-of-demeter-wikilink]. Yes I know it's wikipedia
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

This already pretty much is what Java allows you with it's access modifiers and they way you access
references, so if you implemented your program resorting to correct data hiding, you will probably
consequently achieve a great encapsulation.

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

One being what we can specifically call "Composition", in which the idea is that the relationship is
so strong that the external class is made up of the classes it "owns", and those can not exist
without the containing class.

The other we call "Aggregation", and the relationship estabilished is not as strong as in the
concept of composition, meaning that the contained class can exist without an instance of the
containing one.

The example in the slides pertains to:

-   A CD contains several Songs and those can't exist (in this example) without an instance of their
    containing class, estabilishing a composition relationship
-   A Car has an Engine but the engine can exist ouside of the car, for example in a boat or
    airplane, meaning that then this is an aggregation relationship, not as strong as the
    composition's one.

A good example could be that for instance a person who has a dog is an aggregation
scenario. The dog makes sense as an entity on his own, and the person is not in fact "composed" of a
dog. An example of a car and it's parts (say, a steering wheel, the seats, the axis, the wheels) is
actually ( _**in my opinion**_ ) a great one for composition, as a car is actually made up of the
combining of all its parts.

Despite this difference, we refer to both quite interchangeably as Composition, and they both create
an `HAS-A` relationship

&nbsp;

## 1.8. Inheritance

A relationship that allows for classes to subclass one another, in order to create a `IS-A`
relationship.

_**The main purpose of this mechanic is to allow for code resuse.**_

A subclass of a given class will inherit all of its parents properties and methods, which will allow
for the reusing of code with little to no modification at all.  
Subclassing should be the tool to use in case you are dealing with a situation in which a specific
class represents a more specific type of another, meaning that it should **know** and **be** all
that the superclass knows and is, otherwise you probably are looking at a situation that is more
suited for composition. Remember that inheritance is a static and very high-coupling relationship,
as you can't choose what to inherit when extending a given class.

Consider inheritance to be more of a code re-utilization tool than of a tool for implementing
Polymorphism, but more on that a bit later, when we discuss that pillar in specific.

&nbsp;

## 1.9. Inheritance vs Composition

Here's the same table that we have in the slides comparing the both:

|               |      Inheritance      |       Composition |
| ------------- | :-------------------: | ----------------: |
| Relation      | static (compile-time) | dynamic (runtime) |
| Encapsulation |       is broken       |        is favored |
| Coupling      |         high          |               low |
| Cohesion      |          low          |              high |
| Boilerplate   |          low          |              high |

Let's go for an explanation of each field:

-   **Relation** refers to when the relationship between the objects is created. The fact that in
    Inheritance it is created during compilation means that this is a relationship that can't even
    change during the execution of my program. A composition relationship is only created during
    runtime, even if I am to never change the reference to any other object, because objects only
    exist when runtime is ocurring.
-   **Encapsulation** refers to how much this is favored in each. In Inheritance, since you get all
    of the properties and behaviours from the superclass, encapsulation isn't enforced, while in
    composition you get to manage it. - REMEMBER THE WORD HISTOGRAM EXERCISE DONE WITH
    INHERITANCE/COMPOSITION
-   **Coupling** refers to how tightly the envolved classes get coupled. In inheritance the coupling
    is obviously way bigger than in composition, as it creates a relation that is unbreakable, when
    on the other hand composition allows me to change what objects are coupled to each other during
    runtime if I so wish.
-   **Cohesion** refers to how much coherence I can get in my classes. Composition allows for very
    coherent classes, that are very specialized at doing one type of task and one type of task
    only. - REMEMBER THE WORD HISTOGRAM EXERCISE DONE WITH INHERITANCE/COMPOSITION
-   **Boilerplate** referrs to how much code I have to write in order to make use of each of these,
    and it's quite obvious that I have to write more in composition, as in inheritance I get all the
    behaviour by just writing `extends <Class>` (imagine that your intent is to create a class that
    does all the same that class X does, plus more. For example if in the word histogram the goal
    really was to have a class that did all that a Map does, plus more. You can create that exact
    behaviour by using composition but not on ly you have to implement the extra methods you want,
    you actually have to create all the other methods that simply would delegate the contained map).
    This might seem like a disadvantage but actually allows me much more control over how my objects
    behave and interact.

You should strive to only use inheritance when the relationship between classes is very clearly an
hierarchical one that is taking full advantage of the mechanic.

**Always favor Composition over Inheritance!!**

&nbsp;

## 1.10. Polymorphism

Polymorphism obviously comes from the conjunction of poly - many - and morphism - forms. Obviously
the concept is tightly related to that idea, that "one given thing can take several forms".

Through Inheritance we can get to make use of polymorphism which is one of the most powerful tools
avaliable in an OOP environment. This is also true for the use of Interfaces in the case of Java,
which allow us to get that polymorphic behaviour on steroids and really see it's full potential and
power.

But why do we have interfaces and not multiple inheritance if Polymorphism is such a powerhammer?

## 1.11. Polymorphism and Single Inheritance

So the Java language does not allow for mutiple inheritance. This is because the creators decided
that they simply did not want to deal with the ["Diamond Problem"][diamond-problem-wiki]. So they
went ahead and gave you another subtyping tool which are interfaces, that do not cause this problem.

Since interfaces do not provide default implementation for any methods because all they do is
implement abstract methods, if two of them actually have "colliding" methods there's no problem, as
the concrete class will be forced to give it it's implementation either way.

_**Just interesting stuff ahead**_  

&nbsp;

Interfaces, as stated previously, were the first way that Java dealt with the decision of not
allowing for multiple inheritance scenarios, and as such the fact that a class implements an
interface makes it become a subtype of that interface... But not a subclass. Which means that you
can get all that sweet, sweet polymorphic behaviour with those.

If you want to read more on it, you can check out the [Liskov substitution
principle][liskov-principle-link], or more on [subtype schemes][subtype-schemes-link]. Also read
into the [relationship between subtyping and inheritance][subtype-relation-with-inheritance]

Modern Java (8 and beyond) actually has features that allow for this problem to appear (Interfaces
can have default implementations) and be dealt with (from wikipedia's article):

> Java 8 introduces default methods on interfaces. If A,B,C are interfaces, B,C can each provide a
> different implementation to an abstract method of A, causing the diamond problem. Either class D
> must reimplement the method (the body of which can simply forward the call to one of the super
> implementations), or the ambiguity will be rejected as a compile error.[6] Prior to Java 8, Java
> was not subject to the Diamond problem risk because it did not support multiple inheritance and
> interface default methods were not available.

All of this to say that, by implementing an Interface, a class becomes a subtype of said interface
allowing it to **be** of several types.

&nbsp;

**Ok, with those interesting things about subtyping out of the way, let's get back on the subject of
Polymorphism.**

Polymorphism is the capability of actually having the compliler delay the binding of the actual code
to the method call up until runtime, instead of doing it right at compile time (which would be
static binding). Or we can simply say "the ability of delaying to runtime the decision of what
method to call". This is a concept also known as **dynamic** or **late binding**.

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
    will be created declaratively, responding to data binding and no more. The pattern we will
    implement in our JavaBank is an MVP pattern.

![mvp-flow][mvp-flow-image]

-   MVVM attempts to separate the development of UI's from the aplication behaviour and business
    logic by making sure that the view only has data bindings to the view-model, which allows for
    complete separation of work on view from other layers.

![mvvm-flow][mvvm-flow-image]

This pattern works by having possibly an Obsever pattern implemented between the `Views` and
`ViewModel` (depending on language specifics, etc), and the general idea is that whenever a change
is performed on the data, the `ViewModel` notifies his observers, and they update themselves by
reading the properties of the `ViewModel`.  
In the example scheme we see that `Binder` entity. I decided to include it in here, as in order to
create an MVVM pattern in Java, we would have to create all the code "gluing" the `View` and
`ViewModel`, very probably in an external entity as the idea is that the `ViewModel` is supposed to
be an entity that simply maps our data into a way for the views to be able to access it. (Apparently
Microsoft loves this pattern, as I found a ton of books on the subject but related to C# and WPF
(Windows Presentation Foundation). Xamarin seems to also have this pattern in mind)

MVVM is a bit of a weird implementation compared to what we are used to look at/work with here at
the bootcamps, so in order to try to help making the concept a bit clearer, here are some possibly
intteresting reads: maybe take a quick glance at [this][mvvm-wikilink] (wiki),
[this][implementing-mvvm-blog-link] (a post about implementing MVVM), or at [ZK(wikipedia
link)][zk-wikilink][(ZK website)][zk-official-link], a Java framework for implementing the MVVM
pattern. An interesting [blog post][anti-mvvm-blog-link] against the use of MVVM, or [another
one][second-anti-mvvm-blog-link].

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
[diamond-problem-wiki]: https://en.wikipedia.org/wiki/Multiple_inheritance#The_diamond_problem
[liskov-principle-link]: https://en.wikipedia.org/wiki/Liskov_substitution_principle
[subtype-schemes-link]: https://en.wikipedia.org/wiki/Subtyping#Subtyping_schemes
[subtype-relation-with-inheritance]:
    https://en.wikipedia.org/wiki/Subtyping#Relationship_with_inheritance
[anti-mvvm-blog-link]: http://khanlou.com/2015/12/mvvm-is-not-very-good/
[second-anti-mvvm-blog-link]: https://www.danielhall.io/the-problems-with-mvvm-on-ios
[mvvm-wikilink]: https://en.wikipedia.org/wiki/Model%E2%80%93view%E2%80%93viewmodel
[implementing-mvvm-blog-link]: https://www.objc.io/issues/13-architecture/mvvm/
[zk-wikilink]: https://en.wikipedia.org/wiki/ZK_(framework)
[zk-official-link]: https://www.zkoss.org/
[//]: # 'LINKS TO IMAGES AND SIMILAR RESOURCES'
[abstraction-image]: resources/images/abstraction.png
[not-a-pipe-image]: resources/images/not-a-pipe.jpg
[increasing-abstraction-image]: resources/images/increasing-abstraction.jpg
[object-interface-image]: resources/images/object-interface.jpg
[mvc-flow-image]: resources/images/mvc-flow-drawing.jpeg
[mvp-flow-image]: resources/images/mvp-flow-drawing.jpg
[mvvm-flow-image]: resources/images/mvvm-flow-drawing.jpg
