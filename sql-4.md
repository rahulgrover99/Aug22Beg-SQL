## Practice questions
* [Find customer reference](https://leetcode.com/problems/find-customer-referee/)
* [Big countries](https://leetcode.com/problems/big-countries/)
* [Not Boring Movies](https://leetcode.com/problems/not-boring-movies/)
* [Article Views](https://leetcode.com/problems/article-views-i/)
* [Patients with a condition](https://leetcode.com/problems/patients-with-a-condition/)


```sql
use sakila;

-- BETWEEN operator
-- BOTH VALUES INCLUSIVE
SELECT * FROM film
WHERE release_year BETWEEN 2007 and 2010;



-- Like operator
SELECT * FROM film
WHERE title like '% love' or title like 'love %' or title like '% love %';


SELECT * FROM film
WHERE title = 'love';


-- 'love%love'

-- Won't return null values. 
select * from film where special_features NOT like '%Trailers%' or special_features is null;

-- is null for checking for null

-- order by
SELECT * FROM film ORDER BY release_year desc, title asc;

-- you can specify multiple columns in the order by clause
-- it will first arrange by col1, then by col2, and then so on. 

-- Error Code: 3065. Expression #1 of ORDER BY clause is not in SELECT list, 
-- references column 'sakila.film.release_year' which is not in SELECT list; 
-- this is incompatible with DISTINCT
SELECT DISTINCT title FROM film ORDER BY release_year;

SELECT DISTINCT release_year FROM film ORDER BY release_year DESC;

-- Limit the number of records rendered
SELECT * FROM film ORDER BY film_id DESC LIMIT 5;

-- I want to see the records from 5 - 10.
SELECT * FROM film WHERE release_year > 2006 LIMIT 6 OFFSET 2;


-- Update the release year for the movie with film_id = 1
-- UPDATE table_name
-- SET column_name = val, col2 = val2
-- WHERE column_name = x;

UPDATE film
SET release_year = 2011
WHERE film_id = 1;

SELECT * FROM film WHERE film_id = 1;

-- set release year - 2012, rating = 'G' for film_id = 1
UPDATE film
SET release_year = 2012, rating = 'G'
where film_id = 1;

-- Its possible to omit (remove) the where clause in update, but that would lead
-- the dbms to update all the records in the table with the specified values.


SELECT * FROM aug22beg.batches;

UPDATE aug22beg.batches
SET name = "temp";

-- It might update all the rows of the table which is not desirable.
-- Error Code: 1175. You are using safe update mode and you tried to update a table 
-- without a WHERE that uses a KEY column.  
-- To disable safe mode, toggle the option in Preferences -> SQL Editor and reconnect.




SELECT * FROM film WHERE film_id = 1005;
DELETE FROM film
WHERE film_id = 1005;

CREATE TABLE temp (
	id INT PRIMARY KEY
);

INSERT INTO temp 
values (1), (2);

SELECT * FROM temp;

DELETE FROM temp;

SET SQL_SAFE_UPDATES = 0;

-- Internally drops the schema;
TRUNCATE temp;


-- Schema goes away
DROP TABLE temp;
CREATE TABLE temp (
	id INT PRIMARY KEY
);

```