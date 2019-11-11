![mavenLogo](./images/maven-logo.png)  

#### [Apache Maven Website](https://maven.apache.org/)

Apache Maven is a software project management and comprehension tool. Based on the concept of a project object model (POM), Maven can manage a project's build, reporting and documentation from a central piece of information.

# 1. Introduction

So far, we've been creating Java projects with the help of IntelliJ and according to a set of conventions we taught you.

There's a **`src`** folder organized in **`packages`** containing all our code and a **`lib`** one incase we're working with external libraries.  
Speaking of which, every time we needed a library we'd copy a **`.jar`** containing it to our project, resulting in duplicate files all over our disks and repos _(ie. SimpleGraphics and PromptView)_.
  
As if this wasn't enough, as projects grow dependencies and resources tend to increase and project lifecycle expands _(ie. moves out of development)_, managing it (compiling, testing, packaging and distributing) can become overwhelming for big teams and organizations since ant needs to be told exactly what to do.  
(Remember we provided the build.xml and helped them configure it).

# 2.1 What is Maven

A solution to all of the above, and some more.  
Maven sets a convention on how to build and manage Java projects and abstracts us from defining and configuring everything ourselves.  

Provides an efficient way to manage dependencies by having one local repository containing a single copy of the dependencies we use, allowing us to reuse that copy across all our projects.
Not only that, it allows us to fetch libraries and plugins from a centralized remote repository making it easier to swap versions and managed several dependencies.

Maven comes with a default configuration (super POM) for building files.
So even if you don't need any external resources, you can still use it for the convience of its abstraction over the build process.

And apparently it allows you to build websites:
[How to build a site with Maven - Guide](https://maven.apache.org/guides/mini/guide-site.html)

_Taken from the link above:_

    Maven has several reports that you can add to your web site to display the current state of the project. These reports take the form of plugins, just like those used to build the project.

    There are many standard reports that are available by gleaning information from the POM.
    Currently what is provided by default are:

    Dependencies Report
    Mailing Lists
    Continuous Integration
    Source Repository
    Issue Tracking
    Project Team
    License

# 2.2 Why should I from Maven to Ant

[**List of Features**](https://maven.apache.org/maven-features.html)

**TL;DR: They're not the same.**

While the same level of project management could be achieved with `ant`, Maven provides an out-of-the-box default configuration which helps streamlining software development by abstracting us of configuration details.

Maven allows a project to build using its project object model (POM) and a set of plugins that are shared by all projects using Maven, providing a uniform build system. Once you familiarize yourself with how one Maven project builds you automatically know how all Maven projects build saving you immense amounts of time when trying to navigate many projects.

Remember that default superpom.xml? It sets a convention on how to compile, test, package and distribute source code, but still allows for user customization.

The dependency manager is awesome, reduces file clutter and saves us the trouble of tracking repositories.

_(With the help of IntelliJ, we don't even have to worry about fetching the dependencies ourselves, we just add them to our pom.xml, but more on that later)_

        When using Maven, speaking of a project is speaking in the philosophical sense, beyond a mere collection of files containing code. A project contains configuration files, as well as the developers involved and the roles they play, the defect tracking system, the organization and licenses, the URL of where the project lives, the project's dependencies, and all of the other little pieces that come into play to give code life. It is a one-stop-shop for all things concerning the project. 
        
        In fact, in the Maven world, a project need not contain any code at all, merely a pom.xml.

# 2.3 Project Object Model

[POM Official Documentation](https://maven.apache.org/pom.html)

##### _From the documentation_

    POM stands for "Project Object Model". 
    
    It is an XML representation of a Maven project held in a file named pom.xml.

    The POM contains all necessary information about a project, as well as configurations of plugins to be used during the build process. It is the declarative manifestation of the "who", "what", and "where", while the build lifecycle is the "when" and "how". 

You can check the default superpom [**here**](https://maven.apache.org/pom.html#Quick_Overview)


And it's where the magic happens. Everything related to our project will be configured here.


Note from the doc:
    
    That is not to say that the POM cannot affect the flow of the lifecycle - it can. For example, by configuring the maven-antrun-plugin, one can embed Apache Ant tasks inside of the POM. It is ultimately a declaration, however. Whereas a build.xml tells Ant precisely what to do when it is run (procedural), a POM states its configuration (declarative). If some external force causes the lifecycle to skip the Ant plugin execution, it does not stop the plugins that are executed from doing their magic. This is unlike a build.xml file, where tasks are almost always dependant on the lines executed before it.


# 2.4 Maven Artifact

Basically, anything produced by the build process and the pom itself.
For example, we could configure it to produce the javadoc files automatically aswell.

war, ear, zip, tarball are several popular packaging file formats.

Archetype is a Maven project templating toolkit.
An archetype is defined as _"an original pattern or model from which all other things of the same kind are made"_.
Archetype help authors create Maven project templates for users, and provides users with the means to generate parameterized versions of those project templates.

# 2.5 Maven Plugins

Remember saying that we could do with achieve the same result with ant?  
Its possible because Maven is - at its heart - a plugin execution framework; all work is done by plugins.

Plugins are artifacts that provide goals to Maven. Furthermore, a plugin may have one or more goals wherein each goal represents a capability of that plugin. For example, the Compiler plugin has two goals: compile and testCompile. The former compiles the source code of your main code, while the latter compiles the source code of your test code.

Plugin can execute several task like compile, run our tests, generate documentation, etc.

# 2.6 Maven Lifecycle

[**Lifecycle Documentation**](https://maven.apache.org/guides/introduction/introduction-to-the-lifecycle.html)

Maven is based around the central concept of a build lifecycle. What this means is that the process for building and distributing a particular artifact (project) is clearly defined.

For the person building a project, this means that it is only necessary to learn a small set of commands to build any Maven project, and the POM will ensure they get the results they desired.

For example, the default lifecycle comprises of the following phases

`validate` - validate the project is correct and all necessary information is available

`compile` - compile the source code of the project

`test` - test the compiled source code using a suitable unit testing framework. These tests should not require the code be packaged or deployed

`package` - take the compiled code and package it in its distributable format, such as a JAR.

`verify` - run any checks on results of integration tests to ensure quality criteria are met

`install` - install the package into the local repository, for use as a dependency in other projects locally

`deploy` - done in the build environment, copies the final package to the remote repository for sharing with other developers and projects.

# 2.7 Plugins and Lifecycle

Each packaging contains a list of goals to bind to a particular phase.

Plugins can contain information that indicates which lifecycle phase to bind a goal to. Note that adding the plugin on its own is not enough information - you must also specify the goals you want to run as part of your build.

The goals that are configured will be added to the goals already bound to the lifecycle from the packaging selected. If more than one goal is bound to a particular phase, the order used is that those from the packaging are executed first, followed by those configured in the POM.

# 2.8 Maven Coordinates

The three fields act much like an address and timestamp in one. This marks a specific place in a repository, acting like a coordinate system for Maven projects:

    groupId: This is generally unique amongst an organization or a project. For example, all core Maven artifacts do (well, should) live under the groupId org.apache.maven. Group ID's do not necessarily use the dot notation, for example, the junit project. Note that the dot-notated groupId does not have to correspond to the package structure that the project contains. It is, however, a good practice to follow. When stored within a repository, the group acts much like the Java packaging structure does in an operating system. The dots are replaced by OS specific directory separators (such as '/' in Unix) which becomes a relative directory structure from the base repository. In the example given, the org.codehaus.mojo group lives within the directory $M2_REPO/org/codehaus/mojo.

    artifactId: The artifactId is generally the name that the project is known by. Although the groupId is important, people within the group will rarely mention the groupId in discussion (they are often all be the same ID, such as the MojoHaus project groupId: org.codehaus.mojo). It, along with the groupId, creates a key that separates this project from every other project in the world (at least, it should :) ). Along with the groupId, the artifactId fully defines the artifact's living quarters within the repository. In the case of the above project, my-project lives in $M2_REPO/org/codehaus/mojo/my-project.

    version: This is the last piece of the naming puzzle. groupId:artifactId denotes a single project but they cannot delineate which incarnation of that project we are talking about. Do we want the junit:junit of 2018 (version 4.12), or of 2007 (version 3.8.2)? In short: code changes, those changes should be versioned, and this element keeps those versions in line. It is also used within an artifact's repository to separate versions from each other. my-project version 1.0 files live in the directory structure $M2_REPO/org/codehaus/mojo/my-project/1.0.

The three elements given above point to a specific version of a project, letting Maven know who we are dealing with, and when in its software lifecycle we want them.

# 2.9 Directory Structure

Maven also provides uses with a standard directory structure so once we're familiar with one project we can easily jump on to another.
Defines common place for source code, tests and resources.
It features everything we need. NEAT!

# 2.10 { Hands On } Maven Hello World!

    <groupId>org.academiadecodigo.bootcamp</groupId>
    <artifactId>maven-hello-world</artifactId>
    <version>1.0-SNAPSHOT</version>

    <properties>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    </properties>

    <build>
        <plugins>
            <!-- Include Main Class attribute in manifest, use with mvn package -->
            <plugin>
                <artifactId>maven-jar-plugin</artifactId>
                <groupId>org.apache.maven.plugins</groupId>
                <version>2.4</version>
                <configuration>
                    <archive>
                        <manifest>
                            <mainClass>org.academiadecodigo.splicegirls.HelloWorld</mainClass>
                        </manifest>
                    </archive>
                </configuration>
            </plugin>


            <plugin>
            <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <version>2.3.2</version>
                <configuration>
                    <source>1.7</source>
                    <target>1.7</target>
                </configuration>
            </plugin>
        </plugins>
    </build>

[Maven Exercise Docs](https://gitlab.com/ac-bootcamp-materials/bootcamp/blob/master/docs/exercises/module_2_maven.adoc)

# 2.11 Maven Repositories

As we've discussed before, everything gets stored in a local repository.
Plugins and dependencies reside here for the convience of being easily shared and accessed by all our projects, resulting in a single source of truth for our development tools.

This local repo is usually located at `~/.m2`


# 2.12 Dependency Management

By adding a dependency tag to our pom, we're telling Maven these files will be needed for the project. If they don't exist in our local repository, Maven needs to be told to import them. Luckily, IntelliJ helps us with that if auto-import is enabled.


# 2.13 Dependency Scope

Some dependencies will only be used in some phases or stages of our lifecycle. Our production build won't include unit tests to test the code, so probably we don't need to package the test library. On the other hand, during development, we could use different resources/assets to optimize test running and debugging and we don't need to include those in the final build


# 2.14 Assembly Plugin

Responsibile for packaging the code, dependencies, documentation and everything else related to the project into a single, distributable file. YAY! Our project is ready to export!

Won't compile locally installed artifacts like the Prompt-View Library, you'll need shade for that.

            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-shade-plugin</artifactId>
                <version>3.1.0</version>
                <executions>
                    <execution>
                        <phase>package</phase>
                        <goals>
                            <goal>shade</goal>
                        </goals>
                    </execution>
                </executions>
                <configuration>
                    <createDependencyReducedPom>false</createDependencyReducedPom>
                    <transformers>
                        <transformer implementation="org.apache.maven.plugins.shade.resource.ManifestResourceTransformer">
                            <mainClass>org.academiadecodigo.javabank.App</mainClass>
                        </transformer>
                    </transformers>
                </configuration>
            </plugin>

# 2.15 {Hands On} Maven Jar with Dependencies

To install 3rd party jars such as the PromptView, clone the repository, create a jar and then:

`mvn install:install-file -Dfile=path/to/file.jar -DpomFile=path/to/that-file-pom.xml`

[**Reference**](https://maven.apache.org/guides/mini/guide-3rd-party-jars-local.html)

# 2.16 {Exercise} Convert Javabank to Maven


# Version check

Any of the following commands will work.
```
mvn -v
mvn -version
mvn --version
```

And you should see a similar output showing version, install location and Java Version

```
Apache Maven 3.6.2 (40f52333136460af0dc0d7232c0dc0bcf0d9e117; 2019-08-27T16:06:16+01:00)
Maven home: /usr/local/Cellar/maven/3.6.2/libexec
Java version: 12.0.2, vendor: Oracle Corporation, runtime: /Library/Java/JavaVirtualMachines/openjdk-12.0.2.jdk/Contents/Home
Default locale: en_PT, platform encoding: UTF-8
OS name: "mac os x", version: "10.14.5", arch: "x86_64", family: "mac"
```

Case someone doesn't have it
```
brew install maven
```
