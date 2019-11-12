# Class docs, finally!


## 1 - Requirements

To develop these docs, you should be familiar with Markdown formatting language. You can read the documentation written by its creator John Gruber [here][markdown-documentation], and if you need a refresher, [this tutorial][markdown-tutorial] should suffice.  
To write these docs, you can use [MacDown][macdown-website] (`brew cask install macdown`), an editing markdown software that allows you to see how your file is rendered.  
You should also have access to the Trello board where we organize who's in charge of each document. Visit [this][trello-invite] to add yourself to the board.

&nbsp;

### 1.1 - Git flow for doc development

As follows:

1. Clone the [repo][docs-repo] or pull the latest changes
2. Create a new branch matching the name in the directory structure for the doc you want to develop. (So, if I was trying to develop docs for **code-conventions**, that would be the name of the branch.)
3. Edit the appropriate .md file
4. Add, commit and push your changes to your branch
5. Issue a merge request and assign the responsible person to it (Sérgio or Ferrão)
6. Cross your fingers and hope to see your changes in the master soon

&nbsp;

## 2 - Development

### 2.1 - Project structure

This project's structure is just a bunch of directories mimicking the structure we have for our slides. Each **module** has an _index.md_ linking to all the docs for that particular module. 

* [Module 0 - Introduction to Computing Systems and Programming][module-0]
* [Module 1 - Programming in Java][module-1]
* [Module 2 - Advanced Concepts & Tools][module-2]
* [Module 3 - Databases, Frameworks & Web Development][module-3]
* [Module 4 - JavaScript][module-4]

&nbsp;

Each **directory for a specific subject** should have the same structure: 

* an **md file**, which is basically the doc file
* a **resources** directory with two sub-directories (images and videos), where all the resources needed for that doc file should be

![Directory structure][directory-structure]

&nbsp;

### 2.2 - md file structure 

* Make sure to have a lot of links, so that when an mc is using the doc, they can click on them directly, instead of having to go look for it.

* All the visual resources you need should be in the resources directory for that particular class. (this ensures we never have broken links, if a picture is removed from a certain server).

* All links should be reference and not inline. If you need examples, use this README as a template. (this makes it easier to change them later).

> if you're trying to link to files in the resources folder, just wrap the location in <> to convert it to a link	
  
* Use headers appropriately, don't abuse them. Headers lives matter. No, but seriously, we usually use level 2 to identify slide number, and lower levels where appropriate. Using headers appropriately will make it easier to navigate through your doc file later.


## Purpose

* The idea is to have a somewhat organized and standard flow for all the classes given in the bootcamp, consistently accross campuses.

* Not only that, these documents are meant to support master coders (especially new ones) when preparing lectures by providing better documentation and flow for any given class.

* All of these files should start with a *context* section, to help contextualize the subject that we'll be talking about next. 

* Each doc must add **extra** information besides what's on the slides, have frequently asked questions by the cadets, show different code examples for hands-on demonstrations and contain pictures or drawings that can be used when explaining a new concept.

* If you drew an awesome picture in class, make sure to take a picture and upload it to the resources for that class, so that people can later reference it.

* Use and link to outside resources, be it videos, tools, pictures, diagrams, what have you!

> It's always a good idea to reference things that cadets have learned previously.

> They should be written in the 3rd person (we/us), as that's how we should talk when giving a lecture.



[markdown-documentation]: <https://daringfireball.net/projects/markdown>
[markdown-tutorial]: <https://www.markdowntutorial.com>
[trello-invite]: <https://trello.com/invite/b/jbOEmzmj/32bcd7201390cf16aa72385685365f70/docs-development>
[trello-board]: <https://trello.com/b/jbOEmzmj>
[macdown-website]: <https://macdown.uranusjr.com>
[directory-structure]: <resources/images/directory-structure.png>

[docs-repo]: <https://github.com/talefe/notes>

[module-0]: <module-0/index.md>
[module-1]: <module-1/index.md>
[module-2]: <module-2/index.md>
[module-3]: <module-3/index.md>
[module-4]: <module-4/index.md>


