```sql
USE AUG22BEG;

SELECT * FROM STUDENTS;

SELECT COUNT(*) FROM Students;

SELECT COUNT(DISTINCT batch_id) from students;

-- Error Code: 1241. Operand should contain 1 column(s)
-- select count((id, batch_id)) from students;


select count(id), count(batch_id) from students;


-- Error Code: 1055. Expression #1 of SELECT list 
-- is not in GROUP BY clause and contains nonaggregated column
-- 'aug22beg.Students.id' which is not functionally dependent on columns in 
-- GROUP BY clause; this is incompatible with sql_mode=only_full_group_by

SELECT batch_id, COUNT(*), MAX(id)
FROM Students
GROUP BY batch_id;



-- Find number of movies released each year
select * from sakila.film;
SELECT release_year, COUNT(*) as count
FROM sakila.film
WHERE film_id > 995
GROUP BY release_year
order by MAX(length);


```