# 1.1. Principles of OOP programming!

## 1.2. The 4 pillars of OOP

These are:

-   Abstraction
-   Inheritance
-   Polymorphism
-   Encapsulation

&nbsp;

## 1.3. Abstraction!

![abstraction][abstraction-image]

One of the most important pillars behind OOP.  
Abstraction is defined by IEEE (Institute of Electrical and Electronics Engineers) as

> A view of a problem that extracts the essential information relevant to a particular purpose and
> ignores the remainder of the information

The idea here is that through abstraction, we are unable to simplify a problem or a representation
only to the extent of detail that is needed for the problem at hand.

Taking in some inspiration from Sérgio, take a look at the following image

![not-a-pipe][not-a-pipe-image]

Now try and answer the question: What is it that you are looking at?  
You might be tempted to go right ahead and answer that it is a pipe. But is it? Even the sentece itself says otherwise...
If it isn't a pipe what is it that you are currently in the presence of?... 
After some consideration you will probably then get to the conclusion that what you're seeing is a painting. Well, you are right.  But alas you are wrong as well.

In fact you are looking at a photo of a paiting of a pipe. And yet, this was plenty enough for all of us involved to know that we are thinking of a pipe, right?  
Even deeper: the simple mentioning of the word pipe is enough for us to all know what we are talking about.

The entire concept of a language is based on abstraction. Damn that's some *deep shit*.


Ok but but lets take a step back, understand how we got here, and what this whole idea of abstraction means to programming.  
As previously stated, the idea is that we abstract only enough of a problem so that we can handle it.

Say I have 


&nbsp;

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

In a MVP implementation, the flow of handling an event will be the following:

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

[mvc-flow-image]: resources/images/mvc-flow-drawing.jpeg
[mvp-flow-image]: resources/images/mvp-flow-drawing.jpg
[abstraction-image]: resources/images/abstraction.png
[not-a-pipe-image]: resources/images/not-a-pipe.jpg
