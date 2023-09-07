```sql

select * from film;

select * from language;

-- | film_title | language_name | 


-- all columns
select * 
from film join language
on film.language_id = language.language_id;


select film.title, language.name, film.language_id
from film join language
on film.language_id = language.language_id;

select f.title, l.name, f.language_id
from film f join language l
on f.language_id = l.language_id;


select * from film_actor;
select * from actor;
select concat(first_name, '   ', last_name) from actor;

-- | actor_first_name | film_id |

-- figure out the tables that have this information -> film_actor, actor

select a.first_name as actor_first_name, fa.film_id FROM
film_actor as fa JOIN actor as a
ON fa.actor_id = a.actor_id;


-- | actor_id | film_name |
-- film_actor, film

select * from film;

SELECT fa.actor_id, f.title FROM
film_actor as fa JOIN film as f
ON fa.film_id = f.film_id;

-- |actor_name | film_name | 
-- actor_name -> actor
-- film_title -> film
-- 3rd table is intermediate table between actor and film -> film_actor

select * from film_actor;
select * from actor;
select * from film;

select a.first_name, f.title FROM 
actor a 
JOIN 
film_actor fa
ON a.actor_id = fa.actor_id
JOIN 
film f
ON fa.film_id = f.film_id
order by f.title;


-- film | film_actor | actor

```