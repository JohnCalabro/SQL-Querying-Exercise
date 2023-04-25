<!-- PART II:  CODE WARS -->

 <!-- SQL Basics: Simple WHERE and ORDER BY -->

<!-- You should return all people fields where their age is over 50 and order by the age descending -->

SELECT * FROM people
WHERE age > 50
ORDER BY age desc

<!-- SQL Basics: Simple SUM -->

<!-- For this challenge you need to create a simple SUM statement that will sum all the ages. -->

SELECT SUM(age) as ages_added FROM people;


<!-- SQL Basics: Simple MIN / MAX -->

SELECT MIN(age), MAX(age) from people

<!-- Find all active students -->

SELECT * from students WHERE IsActive = 1

<!-- SQL Basics: Simple GROUP BY -->

select age, count(*) as people_count from people group by age;


<!-- SQL Basics: Simple HAVING  -->



SELECT age, count(id) AS total_people
FROM people
GROUP BY age
HAVING count(id) > 9;
