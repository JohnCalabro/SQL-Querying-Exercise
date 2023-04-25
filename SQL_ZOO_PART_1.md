<!-- PART I:

SQL Zoo - Part I:  -->

<!-- Tutorial 0:

1: Modify it to show the population of Germany -->

SELECT population FROM world
  WHERE name = 'Germany'

<!-- 2: Show the name and the population for 'Sweden', 'Norway' and 'Denmark'. -->

SELECT name, population FROM world
  WHERE name IN ('Sweden', 'Norway', 'Denmark');

<!-- 3: Which countries are not too small and not too big? BETWEEN allows range checking (range specified is inclusive of boundary values). The example below shows countries with an area of 250,000-300,000 sq. km. Modify it to show the country and the area for countries with an area between 200,000 and 250,000. -->

SELECT name, area FROM world
  WHERE area BETWEEN 200000 AND 250000


<!-- Tutorial 1: -->

<!-- 1: Find the country that start with Y -->

SELECT name FROM world
  WHERE name LIKE 'Y%'

<!-- 2: Find the countries that end with y -->

SELECT name FROM world
  WHERE name LIKE '%y'

<!-- 3: Find the countries that contain the letter x -->

SELECT name FROM world
  WHERE name LIKE '%x%'

<!-- 4: Find the countries that end with land -->

SELECT name FROM world
  WHERE name LIKE '%land'

<!-- 5: Find the countries that start with C and end with ia -->

SELECT name FROM world
  WHERE name LIKE 'C%' AND name LIKE '%ia'

<!-- 6: Find the country that has oo in the name -->

SELECT name FROM world
  WHERE name LIKE '%oo%'

<!-- 7: Find the countries that have three or more a in the name -->

SELECT name FROM world
  WHERE name LIKE '%a%a%a%';

<!-- 8: Find the countries that have "t" as the second character. -->

SELECT name FROM world
 WHERE name LIKE '_t%'
ORDER BY name

<!-- 9: Find the countries that have two "o" characters separated by two others. -->

SELECT name FROM world
 WHERE name LIKE '%o__o%';

<!-- 10: Find the countries that have exactly four characters. -->

SELECT name FROM world
 WHERE name LIKE '____'


<!-- Tutorial 2: -->

<!-- 1:  Read the notes about this table. Observe the result of running this SQL command to show the name, continent and population of all countries. -->

SELECT name, continent, population FROM world
<!-- 
2: How to use WHERE to filter records. Show the name for the countries that have a population of at least 200 million. 200 million is 200000000, there are eight zeros. -->

SELECT name FROM world
WHERE population >= 200000000

<!-- 3: Give the name and the per capita GDP for those countries with a population of at least 200 million.
HELP:How to calculate per capita GDP
per capita GDP is the GDP divided by the population GDP/population -->

SELECT name, GDP/population FROM world
WHERE population >= 200000000

<!-- 4: Show the name and population in millions for the countries of the continent 'South America'. Divide the population by 1000000 to get population in millions. -->

SELECT name, population/1000000 FROM world
WHERE continent = 'South America'

<!-- 5: Show the name and population for France, Germany, Italy -->

SELECT name, population FROM world WHERE name in ('France', 'Germany', 'Italy')

<!-- 6: Show the countries which have a name that includes the word 'United' -->

SELECT name FROM world WHERE name LIKE '%United%'

<!-- 7: Show the countries that are big by area or big by population. Show name, population and area. -->

SELECT name, population, area FROM world WHERE
area > 3000000 OR population > 250000000

<!-- 8: Exclusive OR (XOR). Show the countries that are big by area (more than 3 million) or big by population (more than 250 million) but not both. Show name, population and area.
* Australia has a big area but a small population, it should be included.
* Indonesia has a big population but a small area, it should be included.
* China has a big population and big area, it should be excluded.
* United Kingdom has a small population and a small area, it should be excluded. -->


SELECT name, population, area
FROM world
WHERE area > 3000000 AND population < 250000000
  OR area < 3000000 and population > 250000000

<!-- 9:Show the name and population in millions and the GDP in billions for the countries of the continent 'South America'. Use the ROUND function to show the values to two decimal places.
For South America show population in millions and GDP in billions both to 2 decimal places. -->


SELECT name, ROUND(population/1000000,2), ROUND(GDP/10000000,2) from world
WHERE continent = 'South America'

<!-- 10: Show per-capita GDP for the trillion dollar countries to the nearest $1000. -->

SELECT name, ROUND(gdp/population, -3)
FROM world
WHERE gdp > 1000000000000

<!-- 11: Show the name and capital where the name and the capital have the same number of characters. -->

SELECT name, capital FROM world WHERE LEN(name) = LEN(capital);

<!-- 12: Show the name and the capital where the first letters of each match. Don't include countries where the name and the capital are the same word. -->

SELECT name, capital
FROM world WHERE LEFT(name,1) = LEFT(capital,1) AND name <> capital

<!-- 13: Find the country that has all the vowels and no spaces in its name. -->

SELECT name FROM world 
WHERE name LIKE '%a%'
AND name LIKE '%e%'
AND name LIKE '%i%'
AND name LIKE '%o%'
AND name LIKE '%u%'
AND name NOT LIKE '% %'


<!-- Tutorial 3:

1: Change the query shown so that it displays Nobel prizes for 1950. -->

SELECT yr, subject, winner
  FROM nobel
 WHERE yr = 1950

<!-- 2: Show who won the 1962 prize for literature. -->

SELECT winner
  FROM nobel
 WHERE yr = 1962
   AND subject = 'literature'

<!-- 3: Show the year and subject that won 'Albert Einstein' his prize. -->

SELECT yr, subject from nobel
WHERE winner =  'Albert Einstein'

<!-- 4: Give the name of the 'peace' winners since the year 2000, including 2000. -->

SELECT winner winner_peace FROM nobel
WHERE subject = 'Peace'
AND yr >= 2000

<!-- 5: Show all details (yr, subject, winner) of the literature prize winners for 1980 to 1989 inclusive. -->

SELECT yr, subject, winner from nobel
WHERE subject = 'literature'
AND yr >= 1980
AND yr <= 1989

<!-- 6: Show all details of the presidential winners -->

SELECT yr, subject, winner FROM Nobel
WHERE winner = 'Theodore Roosevelt'
OR winner = 'Woodrow Wilson'
OR winner = 'Jimmy Carter'
OR winner = 'Barack Obama'

<!-- 7: Show the winners with first name John -->

SELECT winner FROM nobel
WHERE winner LIKE 'John%'

<!-- 8: Show the year, subject, and name of physics winners for 1980 together with the chemistry winners for 1984. -->

SELECT yr, subject, winner FROM nobel
WHERE subject = 'physics'
AND yr = '1980'
OR subject = 'chemistry'
AND yr = '1984'

<!-- 9: Show the year, subject, and name of winners for 1980 excluding chemistry and medicine -->

SELECT yr, subject, winner from  nobel
WHERE yr = '1980'
AND subject != 'chemistry'
And subject != 'medicine'

<!-- 10: Show year, subject, and name of people who won a 'Medicine' prize in an early year (before 1910, not including 1910) together with winners of a 'Literature' prize in a later year (after 2004, including 2004) -->

SELECT yr, subject, winner from nobel
WHERE subject = 'medicine'
AND yr < '1910'
OR subject = 'literature'
AND yr >= '2004'

<!-- 11: Find all details of the prize won by PETER GRÜNBERG -->

SELECT yr, subject, winner from nobel
WHERE winner = 'Peter Grünberg'

<!-- 12: Find all details of the prize won by EUGENE O'NEILL -->

SELECT yr, subject, winner from nobel
WHERE winner = 'Eugene O''Neill'

<!-- 13: Knights in order
List the winners, year and subject where the winner starts with Sir. Show the the most recent first, then by name order. -->


SELECT winner, yr, subject
FROM nobel
WHERE winner LIKE 'sir%'
ORDER BY yr DESC, winner

<!-- 14: The expression subject IN ('chemistry','physics') can be used as a value - it will be 0 or 1.
Show the 1984 winners and subject ordered by subject and winner name; but list chemistry and physics last. -->


SELECT winner, subject, subject IN ('physics','chemistry')
  FROM nobel
 WHERE yr=1984
 ORDER BY subject,winner