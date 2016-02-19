---
title: Tools
layout: develop
level: 1
---

IDE
-------------------------------------------------

You may use any IDE you want but as I tested some of the popular free ones I
had little till no support for CoffeeScript, Jade and other modern dialects.
So you may use some generic IDEs like Eclipse or NetBeans with less support or
some simpler Editors which often at least has a working syntax highlighting.

I for myself decided to use Sublime_Text which is a Texteditor with lots of
modules, Syntax Highlighting, Linting, GIT integration and lots more in a
fast way.

To get a good support I installed the following modules:

- PackageControl
- CoffeeScript
- SublimeGit
- SublimeLinter


Build Tool
-------------------------------------------------

To best support the developer and make the daily tasks and calls to the
different tools like git, coffee, mocha... slim and easy I use the
[Builder](https://alinex.github.io/node-builder/) tool.


Operating System
-------------------------------------------------

The alinex modules are developed and tested only on UNIX operating systems
like Linux or Mac OSX. In general it should also work on Windows but it's
neither tested.


Test Coverage
-------------------------------------------------

As far as possible I try to make a complete test coverage with unit tests
and additional end to end test where possible.


Continuous Integration
-------------------------------------------------

Most modules will use the travis continuous integration service. If this is
done a badge image should be added in the main README.md.
