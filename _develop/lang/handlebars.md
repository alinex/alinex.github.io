---
title: Handlebars Templates
layout: develop
---

Handlebars is a simple web template system with minimal logic support. The
templates written in this language will be compiled and executed with specific
context to get the result. It's main purpose is for html output but can be used
for other text based formats, too.

An template may look like:

  <ul>  
  {{#each users}}
      <li>{% raw %}pMore fixes.{{firstname}} {{lastname}}{% endraw %}</li>      
  {{/each}}
  </ul>

Expression Syntax
===================================================================
The Handlebars Expressions like seen above are written like (a double stash before,
followed with the content to be evaluated, followed by a closing double stash): 

    {% raw %}
    {{ content goes here }}
    {% endraw %}

Special HTML characters are escaped automatically, but you may prevent this
with the following syntax:

    {% raw %}
    Triple Stash {{{ }}} For Non-escape HTML
    {% endraw %}

The content may be a variable to use, some control methods or special helper
functions to include.

Comments
-------------------------------------------------------------------
This is how you add comments in a Handlebars template:

    {% raw %}
    {{! Whatever is inside this comment expression will not be outputted  }}
    {% endraw %}

Instead of the regular html comments they will not be outputted to the user.

Blocks
-------------------------------------------------------------------
Blocks in Handlebars are expression that has a block, an opening `{{# }}`
followed by a closing `{{/ }}`. See some more examples below.

    {% raw %}
    {{#each}}Content goes here.{{/each}}
    {% endraw %}

Here is an if block

    {% raw %}
    {{#if someValueIsTrue}}Content goes here{{/if}}
    {% endraw %}

Helpers
--------------------------------------------------------------------
An helper is an additional method working with some content or variable. They
may be used as simple functions or block expressions or both depending on it's
implementation.

Inline helpers are used as:

    {% raw %}
    {{helperName arg1 arg2 arg3}}
    {% endraw %}

Block helpers are used as:

    {% raw %}
    {{#helperName arg 1 arg2}}
    other stuff
    {{/helperName}}
    {% endraw %}

Paths (with dot notation)
--------------------------------------------------------------------
A path in Handlebars is a property lookup. If we have a name property that
contains an object, such as:

    {% raw %}
    objData = {name: {firstName: "Michael", lastName:"Jackson"}}
    {% endraw %}

We can use nested paths (dot notation) to lookup the property you want, like this:

    {% raw %}
    {{name.firstName}}
    {% endraw %}

### Parent Path ../
Handlebars also has a parent path ../ to lookup properties on parents of the
current context. Thus with a data object such as this:

    {% raw %}
    shoesData = {groupName:"Celebrities", users:[{name:{firstName:"Mike", lastName:"Alexander" }}, {name:{firstName:"John", lastName:"Waters" }} ]};
    {% endraw %}

We can use the parent path ../ to get the groupName property:

    {% raw %}
    ​<script id="shoe-template" type="x-handlebars-template">​
       {{#users}}​
        <li>{{name.firstName}} {{name.lastName}} is in the {{../groupName}} group.</li>​
        {{/users}}
    ​</script>
    {% endraw %}
