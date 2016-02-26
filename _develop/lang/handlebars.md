---
title: Handlebars Templates
layout: develop
---

Handlebars is a simple web template system with minimal logic support. The
templates written in this language will be compiled and executed with specific
context to get the result. It's main purpose is for html output but can be used
for other text based formats, too.

An template may look like:

``` html
<ul>
{{#each users}}
    <li>{{firstname}} {{lastname}}</li>
{{/each}}
</ul>
```

Expression Syntax
===================================================================
The Handlebars Expressions like seen above are written like (a double stash before,
followed with the content to be evaluated, followed by a closing double stash): 

    {% raw %}
    {{ content goes here }}
    {% endraw %}

Special HTML characters are escaped automatically, but you may prevent this
with the following syntax:

    Triple Stash {{{ }}} For Non-escape HTML

The content may be a variable to use, some control methods or special helper
functions to include.

Comments
-------------------------------------------------------------------
This is how you add comments in a Handlebars template:

    {{! Whatever is inside this comment expression will not be outputted  }}

Instead of the regular html comments they will not be outputted to the user.

Blocks
-------------------------------------------------------------------
Blocks in Handlebars are expression that has a block, an opening `{{# }}`
followed by a closing `{{/ }}`. See some more examples below.

    {{#each}}Content goes here.{{/each}}

Here is an if block

    {{#if someValueIsTrue}}Content goes here{{/if}}

Helpers
--------------------------------------------------------------------
An helper is an additional method working with some content or variable. They
may be used as simple functions or block expressions or both depending on it's
implementation.

Inline helpers are used as:

    {{helperName arg1 arg2 arg3}}

Block helpers are used as:

    {{#helperName arg 1 arg2}}
    other stuff
    {{/helperName}}

Paths (with dot notation)
--------------------------------------------------------------------
A path in Handlebars is a property lookup. If we have a name property that
contains an object, such as:

    objData = {name: {firstName: "Michael", lastName:"Jackson"}}

We can use nested paths (dot notation) to lookup the property you want, like this:

    {{name.firstName}}

### Parent Path ../
Handlebars also has a parent path ../ to lookup properties on parents of the
current context. Thus with a data object such as this:

    shoesData = {groupName:"Celebrities", users:[{name:{firstName:"Mike", lastName:"Alexander" }}, {name:{firstName:"John", lastName:"Waters" }} ]};

We can use the parent path ../ to get the groupName property:

    ​<script id="shoe-template" type="x-handlebars-template">​
       {{#users}}​
        <li>{{name.firstName}} {{name.lastName}} is in the {{../groupName}} group.</li>​
        {{/users}}
    ​</script>
