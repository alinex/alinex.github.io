---
title: Working with Data Structures
layout: post
tags: NodeJS Object YAML XML INI Tables
---

All of my applications need complex data structures in many places. They are used
as configuration, parameter or database query results. On them I need to validate,
transform, format, join, filter and output in different formats.

To do these I had to implement the above functionality and as I saw the code
duplication I created I had to optimize it. So I used my recently two weeks of
hollidays to extract this features into two multifunctional modules:

- [Formatter](http://alinex.github.io/node-formatter) to read and write data
  structures from text elements
- [Table](http://alinex.github.io/node-table) to work with table like data which
  is represented with columns and rows

Just now the new modules are ready to use with all planed features available.

In the next weeks I will integrate this two modules into my applications and
my other modules the next weeks.


Formatter
----------------------------------------------------------
Find it at [Formatter](http://alinex.github.io/node-formatter)

It is an easy way to serialize and deserialize different data
objects into multiple formats like:

- JSON    
- JS      
- CSON    
- Coffee  
- YAML    
- INI     
- Properties
- XML     
- BSON    
- CSV     

This is done using different helpers for each format which are installed as
sub packages. But on runtime only the needed libraries are loaded on demand.

Each format supports a `parse` and `stringify` method sometimes with some options.
So you can transform each format from and to an object structure and therefore also
transform from one to another format.


Table
----------------------------------------------------------
Find it at [Table](http://alinex.github.io/node-table)

This package defines an object type table which can be created out of a array of
arrays or a record structure like from a relational database.

With this table you may easily work and append, join, sort, filter, rename and
format it's content's. The result maybe transformed or directly added to a report
or be exported into CSV using the formatter.
