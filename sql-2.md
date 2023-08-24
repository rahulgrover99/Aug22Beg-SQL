### Keys
Keys are used to 
* uniquely identify a tuple in a relation.
* describe relationships between relations.

How can you uniquely identify a student in the students relation?
> Student (name, age, address, phone, email)

* Name
  * A name might not be unique
* Phone or Email
  * Each student will have a unique phone or email address

#### Super keys

A set of attributes that uniquely identify a tuple in a relation.

For our student relation `Student (name, age, address, phone, email)`, following are some super keys:
* `{id, name}`
* `{id, name, phone}`
* `{id, name, email}`
* `{id, name, email, phone}`
* `{id, name, email, phone, age, address}`
* `{id}`

#### Candidate keys

A **minimal** set of attributes that uniquely identify a tuple in a relation.

For example `{id, name, email, phone}` is a super key but is it a candidate key?

**No**, since you can remove `phone` or any other attribute set, but it will still uniquely identify a tuple.

A set of candidate keys for our student relation
* id
* phone
* email

#### Primary Keys
> a specific choice of a minimal set of attributes (columns) that uniquely specify a tuple (row) in a relation (table)

> a primary key is a choice of candidate key (a minimal superkey); any other candidate key is an alternate key.

**Each relation can only have one primary key**

#### Composite Keys
Sometime you want to use multiple attributes to uniquely identify a tuple. For example, you might want to use a combination of name and phone number to uniquely identify a student.

Composite keys are used in mapping tables. For instance, you might want to have a relation for student feedback.
You could use `student_id` and `batch_id` for uniquely identifying a tuple.

#### Foreign Keys
> A Foreign Key is a database key that is used to link two tables together
> A foreign key is a set of attributes in a table that refers to the primary key of another table

Imagine adding a batch to a student.
You could add all the column for a batch in the student relation.

| Name | Email | Phone | Age | Address | Batch Name | Batch | Start Date | Type |
| ---- | ----- | ----- | --- | ------- | ---------- | ----- | ---------- | ---- |

Problem with this solution
* Duplication - All the columns from the batch relation are duplicated
* Integrity - What if the original relation is duplicated?

Can we just reference the original relation?
| Name | Email | Phone | Age | Address | Batch Id |
| ---- | ----- | ----- | --- | ------- | -------- |


## Some queries to get you started

```sql 
-- RDBMS 
-- MySql -> RDBMS
-- Workbench -> IDE helps us interact with MySql Server

CREATE DATABASE aug22beg;

show databases;

-- Not case sensitive

-- Execute the command Cmd+Enter

-- Backticks are used to separate out db names, table names
-- from the SQL reserved keywords
-- CREATE DATABASE `database` -> Would work.

-- Deleting a database. 
-- DROP DATABASE aug22Beg;


-- INSERT INTO `aug22beg`.`students` (`id`, `name`) VALUES (2, 'Sandipan');
-- Error Code: 1062. Duplicate entry '2' for key 'students.PRIMARY'

CREATE TABLE `aug22beg`.`batches`(
	`id` INT PRIMARY KEY NOT NULL,
    `name` varchar(50)
);

INSERT INTO `aug22beg`.`batches` (`id`, `name`) VALUES (1, 'Aug22 Beg');
INSERT INTO `aug22beg`.`batches` (`id`, `name`) VALUES (2, 'Aug23 Beg');


CREATE TABLE `aug22beg`.`students` (
  `id` INT NOT NULL AUTO_INCREMENT,
  `name` VARCHAR(45) NULL,
  `batch_id` INT,
  PRIMARY KEY (`id`),
  FOREIGN KEY (`batch_id`) REFERENCES `aug22beg`.`batches`(`id`)
  );
-- DROP TABLE aug22beg.students;


-- Inserting values into the table
INSERT INTO `aug22beg`.`students` (`id`, `name`, `batch_id`) VALUES (1, 'Rahul', 1);
INSERT INTO `aug22beg`.`students` (`id`, `name`, `batch_id`) VALUES (2, 'Sujay', 3);
-- Error Code: 1452. Cannot add or update a child row: 
-- a foreign key constraint fails (`aug22beg`.`students`, 
-- CONSTRAINT `students_ibfk_1` FOREIGN KEY (`batch_id`)
--  REFERENCES `batches` (`id`))

INSERT INTO `aug22beg`.`students` (`id`, `name`) VALUES (4, 'Naman');
INSERT INTO `aug22beg`.`students` (`id`, `name`) VALUES (3, 'Vishal');


SELECT * FROM aug22beg.students;


```