Authors:

[Rolo](mailto:diogo.rolo@academiadecodigo.org)

&nbsp;

# 1.1. The prompt you can view!

## 1.2. Prompt-view

Prompt view is our very own tiny dear library that allows interactive prompts from the command line.
It provides a small API that makes it simple to learn to use and it is quite useful if all that you
need for your application can be obtained via textual input from the user via the command line.

You can remember the cadets about the importance of using libraries and code bases. By using this
library, we are saving them all the throuble that they would have in implementing all the specific
interactions the user could have with the application, all the trouble they would have to deal with
in order to create for example a menu.

Also, it is quite relevant to let the cadets know that this is an open-source project, hosted
[here][prompt-view-repo] and that they or anyone else for that matter can actually both read the
source code and contribute to it if they find improvements to be made or bugs.(There's already a
contribution from a fellow ex-code cadet, and ad the time of writing these notes, a pull-request is
currently pending, also from an ex-code cadet)  
Mentioning this makes this a good moment to talk about (maybe once more) the relevance of
open-source projects for all of us developers to progress as a whole community.

And a nice quote for you since we're here:  
“A piece of knowledge, unlike a piece of physical property, can be shared by large groups of people
without making anybody poorer.” ― Aaron Swartz

&nbsp;

## 1.3. Be a master of the [_possimpable_][joke-video-url]

This slide lists some of the features of [prompt-view][prompt-view-repo]:

-   You can attach prompt-view to any input or output stream. This means that you are able to
    actually even use prompt-view to interact with a client over a network!
-   Fetch a number imput from your user and validate it
-   Fetch a string from your user and validate it.
-   Creating menus easily from an array of options
-   You can have messages being presented in case the user's input doesn't meet any of your
    validations

&nbsp;

## 2.1. Prompts and scanners!

These are basically the entities that this library is built around in order to achieve it's full
behaviour.

&nbsp;

## 2.2. Scanners

Scanners are the entities that we use in this library in order to represent a question. This means
that those are the enteties that are responsible for defining the message that is shown and the
expected answer type.

Therefore there are several types of scanners in the library, each meant to expect a different type
of input from the user, the possible ones being:

-   Integer
-   PrecisionDouble
-   String
    -   all of the previous present a message and expect the corresponding type as input
-   Menu - this type of scanner presents a message and the previously specified possible options and
    in turn expects an integer representing the chosen option as input.

&nbsp;

## 2.3. Prompt

So, if scanners represent our questions... Prompts represent the act of _prompting_ them to our
user.

As previously stated, this Prompt can be attached to any input and output streams, and will use
these scanners to fetch data.

A single instance of prompt can make as many questions to your user as you wish, it's just a matter
of giving it the specific Scanner to use at the moment of fetching the user's input.

&nbsp;

## 2.4. Q & A time? Prompt me anything

Slide just showing some example usages of the library

&nbsp;

## 2.5. Integer scanning

Integer scanning is done with the usage of `IntegerInputScanner` in case you want to simply ask for
a number, or you can have validations by either a set or a range of numbers by using
`IntegerRangeInputScanner` or `IntegerSetInputScanner`. An `IntegerSetInputScanner` will receive a
`Set` of Integers as constructor argument, and an `IntegerRangeInputScanner` will simply receive the
two values between which answers are accepted.

&nbsp;

## 2.6. Double scanning

The exact same behaviour as `IntegerRangeInputScanner`, except it is prepared to deal with float or
double values.

&nbsp;

## 2.7. Fetching those Strings

In order to ask your user for String type inputs, you can use the `StringInputScanner` class for
"normal" questions.  
You also have avaliable a `PasswordInputScanner` which behaves like the previous scanner, except
that the input will not be displayed as it is being entered (think "unix" type password inputs in
the CLI. Also, keep in mind that this functionality probably will not work on IDE and similar
environments, and the input will be visible.)

There's also the possibility of using a `StringSetInputScanner` which will allow you to validate the
user's input against a given `Set` of strings.

&nbsp;

## 2.8. Create Menus

Prompt-View allows for easy creation of menus. In order to create one, you will need to instantiate
a `MenuInputScanner`. This will in turn need to be given an array of Strings that will be used as
the menu's options, and will be expecting the user input in the form of an Integer.

&nbsp;

## 2.9. You ain't going anywhere until you answer correctly!

![whatdidyousay][whatdidyousay-image]

Questions that have validators and menus will prompt the question to your user over and over if his
answer doesn't meet the criteria your validator is expecting, and you can display an error message
in order to give your user some more information about why his input wasn't valid.

&nbsp;

## 2.10. {Exercise} Prompt-view Login

### Objectives

-   Creating a simple application so that the cadets might familiarize themselves with the
    [Prompt-view][prompt-view-repo] library.

### Flow

1. Show the cadets our solution running so that they can see the expected final behaviour
2. Ask them what entities they think we should have

-   User - abstracts our login credentials
-   UI - abstract tthe interface created with [Prompt-view][prompt-view-repo]
-   UserStore - the actual place where we store our users and access their data

3. Remind the cadets that they have already used external libraries previously and if needed
   remember them how they include one in their project (Have them clone the repository from GitHub
   and package the project themselves, the repository includes a `build.xml` file)

#### Possible problems

-   The `PasswordInputScanner` won't be able to hide the password input unless its being executed
    from a compiled application, meaning the password will be visible on the IDE's console, as
    stated previously
-   Guide the cadets to our structure and make sure they understand each entity's responsability.

[//]: # 'LINKS TO VARIOUS EXTERNAL RESOURCES'
[joke-video-url]: https://youtu.be/sutnLWqngfI?t=90
[//]: # 'LINKS TO IMAGES AND SIMILAR RESOURCES'
[whatdidyousay-image]: resources/images/whatdidyousay.jpeg
[//]: # 'LINKS TO REPOSITORY'
[prompt-view-repo]: https://github.com/academia-de-codigo/prompt-view
