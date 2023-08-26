# CRUD - 1

Reference: Module 2 and Module 3 from https://www.scaler.com/topics/sql/


```sql
INSERT INTO sakila.film VALUES
(1001, 'The Dark Knight', 'Batman fights joker', 2008, 1, NULL,  3, 4.99, 152, 19.99, 'PG-13', 'Trailers', SYSDATE());

-- note that it is not recommended
-- avoided setting value for primary key because auto-generated
-- last updated date is also auto-generated.alter
-- there might be some columns for which you can avoid setting values


INSERT INTO `sakila`.`film` 
(`title`, `description`, release_year, language_id, rental_duration, rental_rate, `length`, replacement_cost, rating)
VALUES
('The Dark Knight - 5', 'Batman fights joker', 2010, 1, 3, 4.99, 152, 19.99, 'PG-13'),
('The Dark Knight - 3', 'Batman fights joker', 2010, 1, 3, 4.99, 152, 19.99, 'PG-13'),
('The Dark Knight - 4', 'Batman fights joker', 2010, 1, 3, 4.99, 152, 19.99, 'PG-13');


-- In this manner, you will able to:
-- 1. Specify values for columns you actually need to.
-- 2. You can specify the values in your own order.


-- Sets the default database in use.
USE sakila;

-- Basic select query
SELECT * FROM film;

-- Only print out selected columns. 
SELECT title as film_title, description as film_description, release_year FROM film;
-- `as` keyword prints out columns with alias names
--  This keyword is used to rename a column or table with an alias. 
-- It is temporary and only lasts until the duration of that particular query

-- Distinct keyword helps you out selecting distinct values from a particular column
SELECT DISTINCT rating FROM sakila.film;


-- Note: DISTINCT keyword must be before all the column names, 
-- as it will find the unique values for the collection of column values. 
-- For example, if there are 2 column names, then it will find distinct pairs
-- among the corresponding values from both the columns.
SELECT DISTINCT rating, release_year FROM sakila.film;



-- DSA LOGIC

-- answer = []
-- for each row in table:
-- 	answer.append(row['col1'], row['col2'])

-- if DISTINCT: 
-- return set(answer)


-- SELECT command without from clause.
SELECT 'HELLO WORLD';
SELECT SYSDATE();

-- Applying functions over columns
SELECT ROUND(length/60, 2) as length_in_hrs FROM film;
SELECT CONCAT(title, ": ", description) from film;

-- Insert data into table from another table

-- CREATE TABLE film_copy (
--   film_id SMALLINT UNSIGNED NOT NULL AUTO_INCREMENT,
--   title VARCHAR(128) NOT NULL,
--   description TEXT DEFAULT NULL,
--   release_year YEAR DEFAULT NULL,
--   language_id TINYINT UNSIGNED NOT NULL,
--   original_language_id TINYINT UNSIGNED DEFAULT NULL,
--   rental_duration TINYINT UNSIGNED NOT NULL DEFAULT 3,
--   rental_rate DECIMAL(4,2) NOT NULL DEFAULT 4.99,
--   length SMALLINT UNSIGNED DEFAULT NULL,
--   replacement_cost DECIMAL(5,2) NOT NULL DEFAULT 19.99,
--   rating ENUM('G','PG','PG-13','R','NC-17') DEFAULT 'G',
--   special_features SET('Trailers','Commentaries','Deleted Scenes','Behind the Scenes') DEFAULT NULL,
--   last_update TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
--   PRIMARY KEY  (film_id)
-- ) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;

INSERT INTO film_copy
(`title`, `description`, release_year, language_id, rental_duration, 
rental_rate, `length`, replacement_cost, rating)
SELECT `title`, `description`, release_year, language_id, rental_duration, 
rental_rate, `length`, replacement_cost, rating FROM film;


-- Display records of films with rating as `PG-13`
SELECT * FROM film WHERE rating = 'PG-13';



-- DSA LOGIC

-- answer = []
-- for each row in table:
-- 	if row matches where clause:
-- 	  answer.append(row['col1'], row['col2'])

-- if DISTINCT: 
-- return set(answer)


-- Display records of films with rating as `PG-13` and release year 2008
SELECT * FROM film WHERE rating = 'PG-13' AND release_year = 2008;

-- Films where release year is not 2006
SELECT * FROM film WHERE NOT release_year = 2006;

-- NOT EQUAL to 
SELECT * FROM film WHERE release_year <> 2006;
SELECT * FROM film WHERE release_year != 2006;

SELECT * FROM film WHERE release_year < 2006;
SELECT * FROM film WHERE release_year <= 2006;

-- Always use parantheses where multiple logical operators used.
SELECT * FROM film WHERE (rating = 'PG-13' OR release_year = 2006) AND rental_rate = 0.99;

-- list might grow long
SELECT * FROM film WHERE rating = 'PG-13' OR rating = 'R' or rating = 'G';


SELECT * FROM film WHERE rating IN ('PG-13', 'R', 'G');




```