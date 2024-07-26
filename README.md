# Project-21-SQL-Commands-PostgreSQL
These are assignments given in Patika Java Intermediate course.


## TASKS

1. How many films have a length greater than the average film length in the film table?
2. How many films have the highest rental_rate in the film table?
3. List the films with the lowest rental_rate and the lowest replacement_cost in the film table.
4. List the customers who made the most purchases in the payment table.



## Queries
```sql

-- TASK 1
SELECT AVG(length) FROM film; -- avg length is 115.27

SELECT * FROM film
WHERE length >
(
    SELECT AVG(length) FROM film
); -- 489 rows total

-- TASK 2
SELECT MAX(rental_rate) FROM film; -- 4.99 is tha max rental rate

SELECT * FROM film
WHERE rental_rate = 
(
    SELECT MAX(rental_rate) FROM film
); -- 336 rows total 

-- TASK 3
SELECT * FROM film
WHERE rental_rate = 
(
    SELECT MIN(rental_rate) FROM film
); -- 341 rows total (checking)

SELECT * FROM film
WHERE replacement_cost = 
(
    SELECT MIN(replacement_cost) FROM film
); -- 41 rows total (checking)
-- main part
(SELECT * FROM film
WHERE rental_rate = 
(
    SELECT MIN(rental_rate) FROM film
)
)
INTERSECT
(SELECT * FROM film
WHERE replacement_cost = 
(
    SELECT MIN(replacement_cost) FROM film
)) -- 15 rows total

-- TASK 4
SELECT COUNT (DISTINCT (customer_id)) FROM customer; -- 599 customers total




SELECT customer.first_name, COUNT (payment.customer_id) AS total, customer.customer_id FROM payment
LEFT JOIN customer ON payment.customer_id = customer.customer_id
GROUP BY customer.customer_id
ORDER BY total DESC; --max 45
-- ORDER BY COUNT(DISTINCT (payment.customer_id)) DESC;



```


### Table for the last Query 
This is the result table for last query (first 30 rows)

```
first_name total, customer_id
Eleanor 45 148
Karl 42 526
Clara 40 144
Marcia 39 236
Marion 39 178
Tammy 39 75
Rhonda 38 137
Curtis 38 410
Tommy 37 459
Brandon 36 366
Elizabeth 35 5
Russell 35 380
Wesley 35 469
Angela 35 29
Louis 34 373
Marsha 34 257
Roger 34 348
Tim 34 468
Lois 34 91
Melissa 34 30
```