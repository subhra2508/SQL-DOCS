# sql queries

### creating database and tables

CREATING DATABASE 
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
SELECT * FROM cats;
```
MULTIPLE INSERT
```SQL
INSERT INTO tablename(column_name,column_name)
VALUES  (value,value),
        (value,value),
        (value,value);
/*EXAMPLE*/
INSERT INTO cats(name,age) values
     ('tony',1),
     ('jira',2),
     ('simsim',3);
```
If you're wondering how to insert a string (VARCHAR) value that contains quotations, then here's how.

You can do it a couple of ways:

Escape the quotes with a backslash: "This text has \"quotes\" in it" or 'This text has \'quotes\' in it'

HOW TO INSERT STRING THAT HAS QUOTES IN IT
```SQL
/*ESCAPE THE QUOTES WITH A BACKSLASH*/
"This text has \"quotes\" in it" or 'This text has \'quotes\' in it'
```
MYSQL WARNINGS
```SQL
SHOW WARNINGS;
```
WANT TO MAKE THE FIELD NOT NULL THEN USE NOT NULL WHILE CREATING THE TABLE :

```SQL
CREATE TABLE cats2(
   name VARCHAR(100) NOT NULL,
   age INT NOT NULL
);
```
CREATING TABLES WITH DEFAULT VALUES :
```SQL
CREATE TABLE cats3 (
   name VARCHAR(20) DEFAULT 'no name provided',
   age INT DEFAULT 99
);
```
PRIMARY KEY :
```sql
CREATE TABLE unique_cats4 (
    cat_id INT NOT NULL AUTO_INCREMENT,
    name VARCHAR(100),
    age INT,
    PRIMARY KEY (cat_id)
);
```
VARIOUS SELECT STATEMENT:

```SQL
SELECT * FROM cats; 

SELECT name FROM cats; 

SELECT age FROM cats; 

SELECT cat_id FROM cats; 

SELECT name, age FROM cats; 

SELECT cat_id, name, age FROM cats; 
```
USE OF WHERE:
```SQL
/*Look the case is not matter*/
SELECT * FROM cats4 where name='skiPpY';
```

INTRODUCTION TO ALIASES:
```SQL
SELECT cat_id as id , name FROM cats4;

DESC cats4;
```
UPDATE DATA :
```SQL
UPDATE cats SET name = 'tony' where age = 3;
```

DELETING DATA :
```SQL
DELETE FROM cats4 WHERE age=2;
/*inorder to delete all */
DELETE FROM cats4;
```
### The World Of String Functions

HOW TO RUN A SQL FILE:
```SQL
CREATE TABLE cats
    (
        cat_id INT NOT NULL AUTO_INCREMENT,
        name VARCHAR(100),
        age INT,
        PRIMARY KEY(cat_id)
    );

/* run these on command line*/
mysql-ctl cli
 
use cat_app;
 
source first_file.sql
 
DESC cats;
```
CREATING A BOOK DATABASE AND LOAD DATA INTO IT :

```SQL
DROP DATABASE IF EXISTS book_shop;
CREATE DATABASE book_shop;
USE book_shop;

CREATE TABLE books(
   book_id INT NOT NULL AUTO INCREMENT,
   title VARCHAR(100),
   author_fname VARCHAR(100),
   author_lname VARCHAR(100),
   released_year INT,
   stock_quantity INT,
   pages INT,
   PRIMARY KEY(book_id)
);

INSERT INTO books (title, author_fname, author_lname, released_year, stock_quantity, pages)
VALUES
('The Namesake', 'Jhumpa', 'Lahiri', 2003, 32, 291),
('Norse Mythology', 'Neil', 'Gaiman',2016, 43, 304);
```
STRINGS FUNCTIONS:
- CONCAT
- SUBSTRING
- REPLACE
- REVERSE
- UPPER AND LOWER
- CHAR LENGTH

CONCAT
```sql
SELECT
  CONCAT(author_fname, ' ', author_lname)
FROM books;
 ```

SUBSTRING
```SQL
SELECT SUBSTRING(title, 1, 10) AS 'short title' FROM books;
```

REPLACE :
```SQL
SELECT    CONCAT   (
       SUBSTRING(title, 1, 10),
       '...'
  ) AS 'short title'
 FROM books;
```

REVERSE
```SQL
SELECT CONCAT(author_fname, REVERSE(author_fname)) FROM books;
```

CHAR LENGTH:
```SQL
SELECT author_lname, CHAR_LENGTH(author_lname) AS 'length' FROM books;
```

UPPER AND LOWER :
```SQL
SELECT CONCAT('MY FAVORITE BOOK IS ', UPPER(title)) FROM books;
 
SELECT CONCAT('MY FAVORITE BOOK IS ', LOWER(title)) FROM books;
```

DISTINCT :
```SQL
SELECT DISTINCT CONCAT(author_fname,' ',author_lname) FROM books;
```
ORDER BY :
```SQL
SELECT title FROM books ORDER BY title;
SELECT author_lname FROM books ORDER BY author_lname DESC;

/*order by title*/
SELECT title, author_fname, author_lname FROM books ORDER BY 1;

/*first sort by author_lname and then sort by author_fname*/
SELECT title, author_fname, author_lname FROM books ORDER BY author_lname author_fname;
```
LIMIT :

```sql
SELECT title, released_year FROM books ORDER BY released_year DESC LIMIT 14;
```
LIKE :
```sql
SELECT * FROM books WHERE author_fname LIKE '%da%';
/* here % (wildcard) means anyting before "da" and anything after "da" are selected */

select title,stock_quantity from books where stock_quantity like '____';
/* here '_ _ _ _' defines four character anything with stock_quantity 4 digits number
(235)234-0987 LIKE '(___)___-____'*/ 

/* so how do i search for the character with _ or % sign on it , we  just use a backslash \ with it*/
select title from books where title like '%\%%';
select title from books where title like '%\_%';
```
COUNT :
```SQL
SELECT COUNT(DISTINCT author_lname) FROM books;
```
GROUP BY:
(summarizes or aggregates identical data into single rows)
```sql
select title,author_lname from books group by author_lname;

/* count how many books is author have using author_lname*/
SELECT author_lname,count(*) FROM books GROUP BY author_lname;
```
MIN AND MAX :
```SQL
SELECT MAX(released_year) FROM books;
SELECT MIN(pages) FROM books;

SELECT title, pages FROM books 
WHERE pages = (SELECT Max(pages) FROM books); 
 
SELECT title, pages FROM books 
WHERE pages = (SELECT Min(pages)  FROM books);

SELECT author_fname, author_lname, Min(released_year) FROM   books 
GROUP  BY author_lname, author_fname;
```