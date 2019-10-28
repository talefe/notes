# Class docs, finally!



## 1. Requirements

To develop these docs, you should be familiar with Markdown formatting language. You can read the documentation written by its creator John Gruber [here][markdown-documentation], and if you need a refresher, [this tutorial][markdown-tutorial] should suffice.  
To write these docs, you can use [MacDown][macdown-website] (`brew cask install macdown`), an editing markdown software that allows you to see how your file is rendered.  
You should also have access to the Trello board where we organize who's in charge of each document. Visit [this][trello-invite] to add yourself to the board.

&nbsp;

## 2. Development

&nbsp;

### 2.1. Project structure

This project structure is just a bunch of directories mimicking the structure we have on our slides. Each **module** has an _index.md_ linking to all the docs for that particular module. 

* [Module 0 - Introduction to Computing Systems and Programming][module-0]
* [Module 1 - Programming in Java][module-1]
* [Module 2 - Advanced Concepts & Tools][module-2]
* [Module 3 - Databases, Frameworks & Web Development][module-3]
* [Module 4 - JavaScript][module-4]

  &nbsp;

Each **directory for a specific subject** has the same structure: 

* an md file, which is basically the doc file
* a directory resources with two sub-directories (images and videos), where all the resources needed for the doc file should be

![Directory structure][directory-structure]



### 2.2. Trello

There is a dedicated [Trello board][trello-board] where all classes are listed, whoever wants it, should add themselves as a member of that card. If you are interested in developing docs already assigned to someone, coordinate with them or pick another one. 

&nbsp;

### 2.3. Git flow

As follows:

1. Clone the [repo][docs-repo] or pull the latest changes
2. Create a new branch matching the name in the directory structure. (So, if I was trying to develop docs for **code-conventions**, that would be the name of the branch.)
3. Edit the appropriate .md file
4. Add, commit and push your changes
5. Issue a merge request and assign the responsible person to it (Sérgio or Ferrão)
6. Cross your fingers and hope to see your changes in the master soon

&nbsp;

## 3. Docs standards

&nbsp;

### 3.1. Formatting rules

* All the visual resources you need should be in the resources directory for that particular class. (this ensures we never have broken links, if a picture is removed from a certain server).

* All links should be reference and not inline. If you need examples, use this README as a template. (this makes it easier to change them later).

	> if you're trying to link to files in the resources folder, just wrap the location in <> to convert it to a link
	
  

* Use headers appropriately, the highest being level 3 and the lowest level 5 (more than that might be overkill, and we don't want more than 3 levels of indentation - eheheh). Using headers appropriately will make it easier to navigate through your doc file later.

&nbsp;

### 3.2. md files organization

* All files should start with a **_context_** section, to help contextualize the subject that we'll be talking about next.
* It should have images and schemes where appropriate. If you did a really cool drawing in class, make sure to take a picture and upload it to the resources for that class, so that later people can reference it.
* Use and link to outside resources, be it videos, tools, pictures, diagrams, what have you!

&nbsp;





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


