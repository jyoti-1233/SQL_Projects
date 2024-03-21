
## Questions and Answers

**Author**: 

**Email**: Jyoti.Thakur

**Website**: https://jyoti-1233.github.io/

**LinkedIn**: https://www.linkedin.com/in/jyoti-thakur-24b6332ab/






/* Q1 Are there museuems without any paintings?*/
````sql
SELECT * FROM museum
left JOIN work ON museum.museum_id = work.museum_id
Where work.work_id is null;


SELECT museum_id FROM museum
Where museum_id not in (SELECT museum_id FROM  work)
````
**Results:**

---------------------------------------------------------------------------------------------


/* Q2 How many paintings have an asking price of more than their regular price?*/

````sql
select count(*) as total
from product_size
WHERE sale_price > regular_price;
````

---------------------------------------------------------------------------------------------
/* Q3 Identify the paintings whose asking price is less than 50% of its regular price*/
````sql

select * from
product_size
WHERE sale_price < (0.5 * regular_price);
````
---------------------------------------------------------------------------------------------
/* Q4:  Which canva size costs the most?*/

````sql
select size_id,label from canvas_size
where size_id = (select size_id from product_size WHERE regular_price = (select MAX(regular_price) from product_size ) )


select c.label, p.sale_price
from
product_size p
JOIN canvas_size c
ON p.size_id = c.size_id
Group by c.label,p.sale_price
HAVING max(p.sale_price)
order by p.sale_price desc


````
---------------------------------------------------------------------------------------------
/* Q5:  Identify the museums with invalid city information in the given datase */

````sql
 SELECT *
FROM museum
WHERE city LIKE '^[0-9]';
````
---------------------------------------------------------------------------------------------


/* Q6:  Identify the museums with invalid city information in the given datase */
/*  Fetch the top 10 most famous painting name */

````sql
select work_id, name from work 
where work_id in (SELECT TOP 10  work_id FROM product_size
order by regular_price desc)
````
---------------------------------------------------------------------------------------------
/* 	Q7 Fetch the top 10 most famous painting subject*/ */

````sql
select top 10  subject, count(*) from subject
group by subject 
order by count(*) desc

select distinct subject, count(*)
from subject s
join work w on s.work_id=w.work_id
group by subject
order by count(*) desc
limit 10;
````

---------------------------------------------------------------------------------------------

/* Q8 How many museums are open every single day? */

````sql
SELECT museum_id,COUNT(museum_id)
FROM museum_hours
GROUP BY museum_id
HAVING COUNT(day) =7
````
---------------------------------------------------------------------------------------------


/* Q9 A Which are the top 5 most popular museum? (Popularity is defined based on most no of paintings in a museum) */

````sql
select top 5 m.museum_id, m.name,
count(*) as no_of_painting
FROM museum m
JOIN work w
ON m.museum_id = w.museum_id
group by m.museum_id, m.name
order by count(*) desc

````
---------------------------------------------------------------------------------------------
/* Q10 Who are the top 5 most popular artist? (Popularity is defined based on most no of paintings done by an artist)*/

````sql
select top 5 artist.artist_id, full_name, nationality, count(work_id) From artist
join work on work.artist_id = artist.artist_id
group by artist.artist_id,full_name,nationality
order by count(work_id) desc
````

---------------------------------------------------------------------------------------------

/* Q11 Which museum is open for the longest during a day. Dispay museum name, state and hours open and which day?*/

````sql
select m.name,m.state, mh.day, mh.open-mh.close as long_e
from museum_hours mh
JOIN museum m
ON mh.museum_id = m.museum_id
order by mh.open-mh.close desc
limit 1
````

---------------------------------------------------------------------------------------------
/* Q12 A Which museum has the most no of most popular painting style?*/

````sql
select top 1 museum.name, style,count(*)  From work
Join museum on museum .museum_id = work.museum_id
where style = (select top 1 style from work 
Group By style
Order by count(*) desc)
Group by museum.name, style
order by count(*) desc





select top 1 m.name, w.style, count(*) as no_of_paint
from museum m
JOIN work w
on m.museum_id = w.museum_id
group by m.name, w.style
order by count(*) desc
````

---------------------------------------------------------------------------------------------
/* Q13 Identify the artists whose paintings are displayed in multiple countries*/

````sql
select top 5 artist.artist_id, artist.full_name,  count(museum.city) From artist
join work on work.artist_id = artist.artist_id
join museum on museum.museum_id = work.museum_id
group by artist.artist_id, artist.full_name
order by count(*) desc
````

--------------------------------------------------------------------------------------------

/* Q14 A Which country has the 5th highest no of paintings?*/

````sql
select m.country, count(*) as no_of_pain
from artist a
JOIN work w ON a.artist_id= w.artist_id
JOIN museum m ON m.museum_id = w.museum_id
group by m.country
order by count(*) desc
LIMIT 1
OFFSET 4
````

--------------------------------------------------------------------------------------------
/* Q15 A Which are the 3 most popular and 3 least popular painting styles?*/

````SQL
(select style, count(*) as no_of_paintings, 'Most Popular' as remarks
from work
group by style
order by count(*) desc
limit 3)

UNION

(select style, count(*) as no_of_paintings, 'Least Popular' as remarks
from work
group by style
order by count(*) asc
limit 3)
;

````

-------------------------------------------------------------------------------------------------