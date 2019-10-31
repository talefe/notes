Authors:

[Rolo](mailto:diogo.rolo@academiadecodigo.org)

&nbsp;

# 1.1. The prompt you can view!

## 1.2. Prompt-view

Prompt view is our very own library that allows interactive prompts from the command line. It
provides a small API that makes it simple to be able to use and it is quite useful if all that you
need for your application can be obtained via textual input from the user via the command line.

You can explain the cadets that the idea of us providing them with such a tool is because this can
be seen as an introduction to working with tools and code that was not developed exclusively by
ourselves, as they will in the future with many other libraries and frameworks. By using this
library, we are saving them all the throuble that they would have in implementing all the specific
interactions the user could have with the application, all the trouble they would have to deal with
in order to create for example a menu with options that the client can navigate with the arrow keys.

Also, it is very relevant to let the cadets know that this is an open-source project, hosted
[here][prompt-view-repo] and that they or anyone else for that matter can actually both read the
source code and contribute to it if they find improvements or bugs.  
Mentioning this makes this a good moment to mention (maybe once more) the relevance of open-source
projects for all of us developers to progress as a whole community.

“A piece of knowledge, unlike a piece of physical property, can be shared by large groups of people
without making anybody poorer.” ― Aaron Swartz

&nbsp;

## 1.3. Be a master of the [_possimpable_][joke-video-url]

This slide lists some of the features of [prompt-view][prompt-view-repo]:

-   You can attach prompt-view to any input or output stream. This means that you are able to
    actually even use prompt-view to interact with a client over a network!
-   Fetch a number imput from your user and validate it
-   Fetch a string from your user and validate it.
-   Creating menus easily from an array of options - something that the cadets will probably
    underestimate, make them notice how much trouble they would have in order to be able to
    implement the same behaviour we are getting if they had to do it themselves.
-   You can have messages being presented in case a user doesn't meet any of your validations

&nbsp;

## 2.1. Prompts and scanners!

These are basically the entities that this library is build around in order to achieve it's full
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

As previously stated, these Prompt can be attached to any input and output streams, and will use
scanners to fetch data.

A single instance of prompt can make as many questions to your user as you wish, it's just a matter
of giving it the specific Scanner to use at the moment of fetching the user's input.

## 2.4. Q & A time? Prompt me anything

[prompt-view-repo]: https://github.com/academia-de-codigo/prompt-view
[joke-video-url]: https://youtu.be/sutnLWqngfI?t=90
