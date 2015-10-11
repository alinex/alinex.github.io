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
use @... for names if used as value
use $... for functions -> more readable
the rest are values
database specific
validator


select: ['@name', '@age'] # fields array
from: '@person'

select: '*'
from: '@person'

select:
  $count: '*'
from: '@person'

# named column
select:
  PersonName: '@name'
select:
  PersonName:
    $count: '*'

# named table
select: '*'
form:
  Person: @person

select: '*'
from:
  Person: @person
  Address:
    address:
      join: 'left'   # left join (default), right, outer, inner
      on:            # join criteria
        ID: '@person.addressID'
        age:
          $gt: 5

select: '*'
from: [
  '@person'
,
  address:
    join: 'left'   # left join (default), right, outer, inner
    on:            # join criteria
      ID: '@person.addressID'
      age:
        $gt: 5
]

# function $distinct $count

where:
  age:
    $or: [15, 30]
  name:
    $like: 'a%' # $or
  age:
    $gt: '@maxage'

group: 'age'
group: [...]

having:

order: 'age'
order: [...]
order:
  num: 'desc'
order: [
  $concat: []
  sort: 'asc'
,
  num: 'asc'
]

limit: 5
offset: 10







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
