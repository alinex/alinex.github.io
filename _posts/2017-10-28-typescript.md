---
title: TypeScript first thoughts
layout: post
tags: nodejs TypeScript
---

After working on my last restructuring with ES.Next + Babel + Flow it felt sometimes
unnaturrally and complicating. Especially the Flow system which was used for
type safety.

So because I neither used TypeScript and it is growing really fast I have to
check it out. But as always I need to use it not only test it. Therefore I decided
to make the rewrite of an earlier unfinished server module using TypeScript.

## TypeScript vs Flow

Both of them will fix the same problems: giving JavaScript type safety. The syntax
of the type definitions is nearly the same but as Flow is made an addition to
JavaScript whoes anotations have to be removed before running, TypeScript is a
superset of JavaScript and will be compiled to JavaScript. This means that the
transformations from Babel are also included into TypeScript.

The big difference for me is that definitions of modules are made more easily, created
alongside the compiled code and are there for nearly any popular module.

## Future

I can't say what the future for TypeScript will bring but it looks promising and
fast growing at the moment. But for my own JavaScript modules I decided to move on
to TypeScript to get more stability and safety.

_Alexander Schilling_
