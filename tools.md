# Software productivity software



# Continuous Integration and Deployment/Build Automation
Continuous integration allows programmers to continuously verify the state of
their software in the process of development by running builds and tests,
often at check-in or daily, depending.

## List of products
### Jenkins
*Self Hosted. https://jenkins.io*

Jenkins is the closest thing to an industry standard. It has a huge list of
plugins available, and it handles multiple levels of automation, dependency
tracking, releases, build systems, etc... Configuration of a build is typically
done through the web interface. Jenkins is typically self-hosted. The list of
things Jenkins can do is too large to attempt to capture here.

If exposing a Jenkins installation to the public internet, care should be taken
to secure it.

Jenkins is a fork from Hudson. Don't bother using Hudson.

### Travis
*Cloud first, Self-Hosted. https://travis-ci.org, https://travis-ci.com*

Travis is also very popular, as it's free to use with open-sourced projects and
integrates well with them on Github (but only github). Configuration is simple,
just edit a yaml file in the root of your project, and then enable that
repository on travis-ci.org. Travis builds in the free tier work good, but
large, slow-compiling codebases may want to pay for service or think of using
Jenkins.

Travis and Jenkins are often used in a complimentary fashion, with Travis
performing quick checks, like style/linting or simple unit tests, and Jenkins
performing an entire test suite, integration tests, and possibly deployment.

Since Travis is entirely driven by configuration file, you don't have much
options to configure the build via a GUI or a web page, but documentation is
generally good. This also means secrets must be stored in your config file.
When it's necessary to use secrets, like for the deployment of a product,
Travis has a feature that will let you encrypt secrets in your config file.
Some users might be weary of this.

Travis performs almost all builds in a docker container. This gives users some
leverage on the environment their build executes in.

### CircleCI
*Cloud first, Self-Hosted. https://circleci.com*

CircleCI is similar to Travis in that it's a hosted service by default. Unlike
Travis, CircleCI works with a variety of code hosting platforms.


### Bamboo
*Self-Hosted, Cloud. https://circleci.com*

Bamboo is an Atlassian product, and as such it can integrate will with their
services, such as Jira. Good things are said about the UI, but it's not as
flexible as Jenkins (but then again, nothing is).

### Gitlab


### Others (TeamCity, Codeship)
Good things are said about both of these, but they have small marketshare and
it's probably more up to taste rather than capability at this point.

Buildbot is also used, though typically as a legacy system.

## Resources
[Jenkins Vs. Bamboo Vs. Travis (*Dated: 1-26-2015*)](https://www.itcentralstation.com/product_reviews/bamboo-review-31830-by-victor-farcic)

[What is the difference between Bamboo, CircleCI, CIsimple/Ship.io, Codeship, Jenkins/Hudson, Semaphoreapp, Shippable, Solano CI, TravisCI and Wercker? (*Quora, Muliple dates*)](https://www.quora.com/What-is-the-difference-between-Bamboo-CircleCI-CIsimple-Ship-io-Codeship-Jenkins-Hudson-Semaphoreapp-Shippable-Solano-CI-TravisCI-and-Wercker)

[Comparison of Continuous Integration Software (*Wikipedia*)](https://en.wikipedia.org/wiki/Comparison_of_continuous_integration_software)


# Build Tools

In general, most of these tools are going to be language specific. Make is the
grandpa in the room and very flexible. There's often overlap between CI and
build tools, so that may be a consideration. There's also often overlap with
devops tools, like Ansible, Chef, Puppet, and SaltStack.

The list of build tools is large, but typically people use one or more of the
following:

* **Make**
* **Maven** (Gradle, sbt, etc...),
* **CMake**
* **SCons**
* **tox** (python)
* **rake** (ruby)

A few tools are more general, and not necessarily oriented around a specific
language.
* **Bazel, Buck, Pants** *(https://bazel.build, https://buckbuild.com/, http://www.pantsbuild.org/)*: These tools all have a common lineage that's
traceable back to Google's Blaze build system. They are generally flexible and
the build system is not specific to any given language.

* **Waf** *(http://waf.io)*: With waf, you write your build scripts as python.
In that sense, it's similar to SCons.


# Code Quality/Static Analysis
There's several different types of checks you can execute to check your code's
quality. You have static analyzers, which parse the code, look at variable
assignments, build call graphs, and generally try to determine where possible
bugs occur. The most prominent examples of these sorts of tools are Coverity,
FindBugs, and Clang Static Analyzer. They find bugs in code that is obviously
compilable, but potentially bad at runtime, like a dereferenced null pointer.

Next up, you have less more rules based code checkers that examine code and look
for obvious and logical errors and/or code that is not compilable. These
are usually faster but per-file. The static analyzer in a typical IDE is
usually somewhere in between the first and second one.

Next, you have coverage checkers, which examine how well your code
is covered by unit tests. Corbertura for Java is a popular example. The services
typically have this integrated into them.

Finally, you have linters, which check/enforce a coding style across your
projects. This typically includes things like  pycodestyle, CheckStyle for Java,
Clang Format, and JSLint. There's different levels of sophistication of tools.
This section will not cover the tools which are built into an IDE, though those
tools vary from linting to full static analysis in capability.


### Coverity
*Cloud, Self-Hosted, https://www.coverity.com/products/coverity-scan/*

Coverity is an industry-standard static analysis tool. It's will check for bugs
in the most popular languages.

Coverity is really two products: Coverity scan (https://scan.coverity.com) is
the free static checker for open-source projects, with checks done in the cloud.
Coverity also has a paid solution which appears to be purchased either based
on the size of the team or lines of code, depending. Coverity is good at
checking for a wide variety of code defects.

Coverity's free product has integration in with Github and Travis.


### Sonarqube
*Self-Hosted, https://www.sonarqube.org/*

Sonarqube is really a platform for code quality checking. It  has very good
integration into CI systems and code hosting platforms. One nice thing
Sonarqube has is analytics on code quality over time. Sonarqube mostly operates
as a reporting tool. It supports a variety of languages, including Java, C++,
Python, PHP, C#, and more. Sonarqube uses some of the open source libraries
underneath to perform the checks.

Others:
* **PMD, FindBugs**: Both of these are Java static analyzers. They are often
compliment each other
* **CPPCheck, Clang Analyzer**: These are similar to PMD and FindBugs.
* **Flake8**: Uses PyFlakes and PEP8 to check code style and find logical
errors, as well as check code complexity.
* **Checkstyle**: Java linter

# Code Review

## Gerritt, GitHub, Crucible/Stash, Phabricator
Github is the one most people are probably familiar with. Gerritt is also very
common in use. Crucible and Stash are Atlassian products. Phabricator is a
a few different things, but it also includes code review. Gerritt is probably
the most powerful of these tools.


# Artifact Repository and Package Management
### Artifactory
*(Self Hosted, https://www.jfrog.com/artifactory/)*


### Nexus 3
*(Self Hosted, http://www.sonatype.org/nexus/category/nexus-3/)*

## Platform/Language Specific and Others
Maven and Conda are sort of language specific. Archiva is a bit more
supporting, but not by much.
* **Maven**
* **Conda**
* **Archiva**
* **PyPI**
* **Bower**
* **yum/rpm**
* **apt/deb**

### Resources
[Binary Repository Manager Feature Matrix *(Date: 9-15-2016)](https://binary-repositories-comparison.github.io/)


# Source Code Management

### Git, Perforce, Subversion, Mercurial, Bazaar, CVS
Most of these need no introduction. Perforce is probably an exception to that,
because it has some unique features. In general, these are effectively in the
order you shuold use them.


 ## Platforms: GitHub, GitLab, BitBucket, Fisheye. Other: (Bazaar, CVS).


# IDEs/Text Editors
Visual Studio, Eclipse, Netbeans, JetBrains Suite (IntelliJ, PyCharm, CLion, etc..).  Other: (Sublime Text, Emacs, Vim, Atom, Notepad++)

# Project Management (Agile), Development Workflows, CCBs, Defects and Issues
Jira, GitHub/GitLab Issues, BugZilla, Trac. Other: (YouTrack, Team Foundation Server, VersionOne)

# Design, Modeling, and Concept Mapping
GenMyModel, Sparx, MagicDraw, Visio, Altova, Omnigraffle, Mindmup

# Debugging, Profiling, Monitoring:
gdb, Allinea, Vampir/VampirTrace, Valgrind, JVM tools. Other: (dtrace, strace, Language and Platform specific tools)

# Notes, Documentation, Technical Notes:
OneNote, Evernote, Jupyter Notebooks, Confluence. Other: (Read The Docs, Language-Specific tools)

# Configuration and Deployment
SaltStack, Ansible, Chef, Puppet, Vagrant, Containers/Docker
