### sql queries

###### creating database and tables
- creating database
``` sql
 SHOW DATABASES;
 CREATE DATABASE <NAME>;
```

TO DROP A DATABASE
``` SQL
DROP DATABASE DATABASE_NAME;
```

USING DATABASES
```SQL
USE <DATABASE NAME>
```

CURRENTLY USING DATABASE
```SQL
SELECT database();
```
CREATING TABLES
```SQL
CREATE TABLE tablename(
column_name data_type,
column_name data_type
);
/*EXAMPLE*/
CREATE TABLE cats
(
   name VARCHAR(100),
   age INT
) 
```

HOW DO WE KNOW IT WORK
```SQL
SHOW TABLES;
SHOW COLUMNS FROM tablename;
/*SHOW COLUMNS DIRECTLY*/
DESC tablename;
```

DROPPING TABLES
```SQL
DROP TABLE tablename;
```
INSERTING DATA
```SQL
INSERT INTO tablename(column_name) VALUES(data);
/*EXAMPLE*/
INSERT INTO cats(name,age) VALUES ('MOE',3);
```
INTRO TO SELECT
```SQL
SELECT FROM cats;
```
MULTIPLE INSERT
```SQL
INSERT INTO tablename(column_name,column_name)
VALUES  (value,value),
        (value,value),
        (value,value);
```

HOW TO INSERT STRING THAT HAS QUOTES IN IT
```SQL
/*ESCAPE THE QUOTES WITH A BACKSLASH*/
"This text has \"quotes\" in it" or 'This text has \'quotes\' in it'
```
MYSQL WARNINGS
```SQL
SHOW WARNINGS;
```








