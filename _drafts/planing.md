Planing
===================

Placeholder Syntax
------------------------

Symbols:
? => used in postgres (shift from array)

number -> insert
string -> insert maybe quoted
date -> format database specific as datetime
object -> using toString()

Object Syntax
---------------------------
use $... for functions -> not neccessary
use @... for names if used as value
the rest are values
database specific
validator


select: ['@name', '@age'] # fields array
from: 'person'

select: '*'
from: 'person'
join: '@address' # full join
join:
  address:
    type: 'left'   # left join (default), right, outer, inner
    on:            # join criteria
      ID: '@person.addressID'
      age:
        gt: 5

# named column
select:
  PersonName: '@name'
select:
  PersonName:
    count: '*'

select: '*'

# named table
from:
  p: 'person'
join:
  address;
    type: 'left'   # left join, right, outer, inner
    alias: '@a'

# function $distinct $count

where:
  age: 30
  name:
    like: 'a%' # $or
  age:
    gt: '@maxage'
order:
  num: 'asc'

#group

limit: 5
offset: 10








So
- plan object call like mongo
-----------------------------------
Mo
- test placeholder syntax
Di
- code object call select
Mi
- code object call update, insert
Do
- test object call
Fr
- server: adding authorization
-----------------------------------
SA
- document database
So
- write blog entry about database with example
