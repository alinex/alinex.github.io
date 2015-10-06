Planing
===================

execute:
DROP TABLE IF EXISTS numbers
CREATE TABLE numbers (
  id INT AUTO_INCREMENT PRIMARY KEY,
  num INT,
  name VARCHAR(10),
  comment VARCHAR(32)
);

execute multiple:
INSERT INTO numbers SET num=1, name='one'
INSERT INTO numbers SET num=2, name='two'
INSERT INTO numbers SET num=3, name='three'

insert one:
INSERT INTO numbers SET num=9, name='nine'

update one record:
UPDATE numbers SET comment='max' WHERE num=9

update multiple:
UPDATE numbers SET comment='ok' WHERE num<9

analysis:
SHOW tables
SHOW columns FROM numbers

query list
SELECT * FROM numbers
query record
SELECT * FROM numbers WHERE num=2
query value
SELECT name FROM numbers WHERE num=2
query field
SELECT name FROM numbers

Mi
- test execute (create, insert, update)
- test query...
- add analysis
Do
- add ssh tunneling support
Fr
- test tunneling only local
-----------------------------------
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