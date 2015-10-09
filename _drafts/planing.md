Planing
===================

Placeholder Syntax
------------------------

Symbols:
? => used in postgres (shift from array)
${name}$ => element from data object
${name.el}$ => sub element from data object

number -> insert
string -> insert maybe quoted
date -> format database specific as datetime
object -> using toString()

Object Syntax
---------------------------
use $... for functions
database specific
validator

select: ['name', 'age'] # fields array
from: 'person'

select: '*'
from: 'person'
join: 'address' # full join
join:
  $left: 'address' # left join, right, outer, inner
  $on:             # join criteria
    ID: 'person.addressID'

# named column
select:
  PersonName: 'name'

# named table
from:
  p: 'person'
join:
  a:
    $left: 'address'

# function $distinct $count

where:
  age: 30
  name:
    $like: 'a%' # $or

order:
  num: 'asc'

#group

limit: 5
offset: 10








Sa
- plan placeholder syntax
- server: adding authorization
So
- plan object call like mongo
-----------------------------------
Mo
- code placeholder syntax
Di
- test placeholder syntax
Mi
- code object call
Do
- test object call
Fr
-----------------------------------
SA
- document database
So
- write blog entry about database with example