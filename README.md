Created my Malaika
# Solutions For Project: SQL ZOO
## SELECT Basics
### Introducing the `world` table of countries
1. 
The example uses a `WHERE` clause to show the population of 'France'. Note that strings (pieces of text that are data) should be in 'single quotes';

Modify it to show the population of Germany
```sql
SELECT population FROM world
  WHERE name = 'Germany';
```
### Scandinavia
2.
Checking a list The word IN allows us to check if an item is in a list. The example shows the name and population for the countries 'Brazil', 'Russia', 'India' and 'China'.

Show the name and the population for 'Sweden', 'Norway' and 'Denmark'.
```sql
SELECT name, population FROM world
  WHERE name IN ('Sweden', 'Norway', 'Denmark');
```
### Just the right size
3.
Which countries are not too small and not too big? `BETWEEN` allows range checking (range specified is inclusive of boundary values). The example below shows countries with an area of 250,000-300,000 sq. km. Modify it to show the country and the area for countries with an area between 200,000 and 250,000.

```sql
SELECT name, area FROM world
  WHERE area BETWEEN 200000 AND 250000;
```
## SELECT from WORLD Tutorial
### Introduction
1.
Read the notes about this table. Observe the result of running this SQL command to show the name, continent and population of all countries.

```sql
SELECT name, continent, population FROM world;
```
### Large Countries
2.
How to use WHERE to filter records. Show the name for the countries that have a population of at least 200 million. 200 million is 200000000, there are eight zeros.

```sql
SELECT name FROM world
WHERE population > 200000000;
```
### Per capita GDP
3.
Give the name and the per capita GDP for those countries with a population of at least 200 million.

```sql
SELECT name,gdp/population FROM world WHERE population > 200000000;
```
### South America In millions
4.
Show the name and population in millions for the countries of the continent 'South America'. Divide the population by 1000000 to get population in millions.

```sql
SELECT name,population/1000000 FROM world WHERE continent = 'South America';
```
### France, Germany, Italy
5.
Show the `name` and `population` for France, Germany, Italy

```sql
SELECT name,population FROM world WHERE name IN ('France','Germany','Italy');
```
### United
6.
Show the countries which have a name that includes the word 'United'

```sql
SELECT name FROM world WHERE name LIKE  '%United%';
```
### Two ways to be big
7.
Two ways to be big: A country is big if it has an area of more than 3 million sq km or it has a population of more than 250 million.

Show the countries that are big by area or big by population. Show name, population and area.

```sql 
SELECT name,population,area FROM world WHERE population > 250000000 OR area > 3000000;
```
### One or the other (but not both)
8.
Exclusive OR (XOR). Show the countries that are big by area or big by population but not both. Show name, population and area.

* Australia has a big area but a small population, it should be **included**.
- Indonesia has a big population but a small area, it should be **included**.
- China has a big population and big area, it should be **excluded**.
+ United Kingdom has a small population and a small area, it should be **excluded**.

```sql
SELECT name,population,area FROM world WHERE (area < 3000000 AND population > 250000000) OR (area > 3000000 and population < 250000000);
```
### Rounding
9.
Show the `name` and `population` in millions and the GDP in billions for the countries of the `continent` 'South America'. Use the `ROUND` function to show the values to two decimal places.

For South America show population in millions and GDP in billions both to **2** decimal places.

```sql
SELECT name, ROUND(population/1000000, 2), ROUND(gdp/1000000000, 2) FROM world WHERE continent = 'South America';
```
### Trillion dollar economies
10.
Show the name and per-capita GDP for those countries with a GDP of at least one trillion (1000000000000; that is 12 zeros). Round this value to the nearest 1000.

Show per-capita GDP for the trillion dollar countries to the nearest $1000.

```sql
SELECT name, ROUND(gdp/population, -3) FROM world WHERE gdp > 1000000000000;
```
### Name and capital have the same length
11.
```sql
SELECT name, capital FROM world WHERE LENGTH(name) = LENGTH(capital);
```
### Matching name and capital
12.
```sql
SELECT name, capital FROM world WHERE LEFT(name, 1) = LEFT(capital, 1) AND name <> capital;
```
### All the vowels
13.
```sql
SELECT name
   FROM world
WHERE name LIKE '%a%'
AND name LIKE '%e%'
AND name LIKE '%i%'
AND name LIKE '%o%'
AND name LIKE '%u%'
AND name NOT LIKE '% %';
```
## SELECT from Nobel Tutorial

### Winners from 1950
1.
```sql
SELECT yr, subject, winner
  FROM nobel
  WHERE yr = 1950
```
### 1962 Literature
2.
```sql
SELECT winner
  FROM nobel
  WHERE yr = 1962
  AND subject = 'Literature
```
### Albert Einstein
3.
```sql
SELECT yr, subject FROM nobel
WHERE winner = 'Albert Einstein';
```
### Recent Peace Prizes
4.
```sql
SELECT winner FROM nobel WHERE subject = 'Peace' AND yr >= 2000
```
### Literature in the 1980's
5.
```sql
SELECT * FROM nobel WHERE subject = 'Literature' AND yr BETWEEN 1980 AND 1989
```
### Only Presidents
6.
```sql
SELECT * FROM nobel
  WHERE winner IN ('Theodore Roosevelt',
                  'Woodrow Wilson',
                  'Jimmy Carter',
                   'Barack Obama');
```
### John
7.
```sql
SELECT winner FROM nobel
WHERE winner LIKE 'John%';
```
### Chemistry and Physics from different years
8.
```sql
SELECT yr, subject, winner FROM nobel
WHERE (yr = 1980 AND subject = 'Physics') OR
 (yr = 1984 AND subject = 'Chemistry');
```
### Exclude Chemists and Medics
9.
```sql
SELECT yr, subject, winner FROM nobel
WHERE subject <> 'Chemistry' AND
subject <> 'Medicine' AND yr = 1980;
```
### Early Medicine, Late Literature
10.
```sql
SELECT yr, subject, winner FROM nobel
WHERE (subject = 'Medicine' AND yr < 1910) OR
(subject = 'Literature' AND yr >= 2004);
```
### Umlaut
11.
```sql
SELECT * FROM nobel WHERE winner = 'PETER GRÜNBERG'
```
### Apostrophe
12.
```sql
SELECT * FROM nobel WHERE winner = "EUGENE O'NEILL";
```
### Knights of the realm
13.
```sql
SELECT winner, yr, subject FROM nobel WHERE winner LIKE 'Sir%' ORDER BY yr DESC;
```

## SELECT within SELECT Tutorial

### List each country name where the population is larger than that of 'Russia'.
1.
```sql
SELECT name FROM world
  WHERE population >
     (SELECT population FROM world
      WHERE name='Russia')
```
### Show the countries in Europe with a per capita GDP greater than 'United Kingdom'.
2.
```sql
SELECT name FROM world WHERE gdp/population >
(SELECT gdp/population FROM world WHERE name = 'United Kingdom')  AND continent = 'Europe'
```
### List the name and continent of countries in the continents containing either Argentina or Australia. Order by name of the country.
3.
```sql
SELECT name, continent FROM world
WHERE continent = (SELECT continent FROM world WHERE name = 'Argentina') OR
continent = (SELECT continent FROM world WHERE name = 'Australia')
ORDER BY name ASC
```
### Which country has a population that is more than Canada but less than Poland? Show the name and the population.
4.
```sql
SELECT name, population FROM world WHERE population > (SELECT population FROM world WHERE name = 'Canada') AND population < (SELECT population FROM world WHERE name = 'Poland')
```
### Show the name and the population of each country in Europe. Show the population as a percentage of the population of Germany.
5.
```sql
SELECT name, CONCAT(ROUND((population/(SELECT population FROM world WHERE name = 'Germany')*100), 0), '%')
FROM world WHERE continent = 'Europe'
```

## SUM and COUNT

### Show the total population of the world.
1.
```sql
SELECT SUM(population)
FROM world
```
### List all the continents - just once each.
2.
```sql
SELECT DISTINCT continent FROM world
```
### Give the total GDP of Africa
3.
```sql
SELECT SUM(gdp) FROM world WHERE continent = 'Africa'
```
### How many countries have an area of at least 1000000
4.
```sql
SELECT COUNT(name) FROM world WHERE area >= 1000000
```
### What is the total population of ('Estonia', 'Latvia', 'Lithuania')
5.
```sql
SELECT SUM(population) FROM world WHERE name IN ('Estonia', 'Latvia', 'Lithuania')
```
### For each continent show the continent and number of countries.
6.
```sql
SELECT continent, COUNT(name) FROM world GROUP BY continent
```
### For each continent show the continent and number of countries with populations of at least 10 million.
7.
```sql
SELECT continent, COUNT(name) FROM world
WHERE population > 10000000
GROUP BY continent
```
### List the continents that have a total population of at least 100 million.
8.
```sql
SELECT continent FROM world
GROUP BY continent
HAVING SUM(population) >= 100000000
```

## JOIN

### Modify it to show the matchid and player name for all goals scored by Germany. To identify German players, check for: teamid = 'GER'
1.
```sql
SELECT matchid, player FROM goal
  WHERE teamid = 'GER'
```
### Show id, stadium, team1, team2 for just game 1012
2.
```sql
SELECT id,stadium,team1,team2
  FROM game WHERE id = 1012
```
### Modify it to show the player, teamid, stadium and mdate and for every German goal.
3.
```sql
SELECT goal.player, goal.teamid, game.stadium, game.mdate
  FROM goal
JOIN game ON (game.id=goal.matchid)
WHERE teamid = 'GER'
```
### Show the team1, team2 and player for every goal scored by a player called Mario player LIKE 'Mario%'
4.
```sql
SELECT game.team1, game.team2, goal.player FROM game
JOIN goal ON game.id = goal.matchid
WHERE player LIKE 'Mario%'
```
### Show player, teamid, coach, gtime for all goals scored in the first 10 minutes gtime<=10
5.
```sql
SELECT goal.player, goal.teamid, eteam.coach, goal.gtime
  FROM goal
JOIN eteam ON goal.teamid = eteam.id
 WHERE gtime<=10
```
### List the the dates of the matches and the name of the team in which 'Fernando Santos' was the team1 coach.
6.
```sql
SELECT game.mdate, eteam.teamname FROM game
JOIN eteam ON game.team1 = eteam.id
WHERE coach = 'Fernando Santos'
```
### List the player for every goal scored in a game where the stadium was 'National Stadium, Warsaw'
7.
```sql
SELECT player FROM goal
JOIN game ON game.id = goal.matchid
WHERE stadium = 'National Stadium, Warsaw'
```
### Instead show the name of all players who scored a goal against Germany.
8.
```sql
SELECT player
  FROM game JOIN goal ON goal.matchid = game.id
    WHERE (game.team1 = 'GER' OR game.team2 = 'GER') AND teamid <> 'GER'
GROUP BY player
```
### Show teamname and the total number of goals scored.
9.
```sql
SELECT teamname, COUNT(player)
  FROM eteam JOIN goal ON id=teamid
GROUP BY teamname
 ORDER BY teamname
```
### Show the stadium and the number of goals scored in each stadium.
10.
```sql
SELECT stadium, COUNT(player) FROM game
JOIN goal ON game.id = goal.matchid
GROUP BY stadium
```
### For every match involving 'POL', show the matchid, date and the number of goals scored.
11.
```sql
SELECT matchid, mdate, COUNT(player)
  FROM game JOIN goal ON goal.matchid = game.id
 WHERE (team1 = 'POL' OR team2 = 'POL')
GROUP BY matchid, mdate
```
### For every match where 'GER' scored, show matchid, match date and the number of goals scored by 'GER'
12.
```sql
SELECT goal.matchid, game.mdate, COUNT(player) FROM goal
JOIN game ON goal.matchid = game.id
WHERE teamid = 'GER'
GROUP BY matchid, mdate
```

## JOIN three tables

### List all of the Star Trek movies, include the id, title and yr (all of these movies include the words Star Trek in the title). Order results by year.
1.
```sql
SELECT movie.id, movie.title, movie.yr FROM movie
WHERE title LIKE '%Star Trek%'
ORDER BY yr
```
### What id number does the actor 'Glenn Close' have?
2.
```sql
SELECT id FROM actor WHERE name = 'Glenn Close'
```
### What is the id of the film 'Casablanca'
3.
```sql
SELECT id FROM movie WHERE title = 'Casablanca'
```
### Obtain the cast list for 'Casablanca'.
6.
```sql
SELECT actor.name FROM actor
JOIN casting ON actor.id = casting.actorid
JOIN movie ON movie.id = casting.movieid
WHERE movie.title = 'Casablanca'
```
### Obtain the cast list for the film 'Alien'
7.
```sql
SELECT name FROM actor
JOIN casting ON actor.id = casting.actorid
JOIN movie ON movie.id = movieid
WHERE movie.title = 'Alien'
```
### List the films in which 'Harrison Ford' has appeared
8.
```sql
SELECT title FROM movie
JOIN casting ON movie.id = casting.movieid
JOIN actor ON actor.id = casting.actorid
WHERE actor.name = 'Harrison Ford'
```
### List the films where 'Harrison Ford' has appeared - but not in the starring role. [Note: the ord field of casting gives the position of the actor. If ord=1 then this actor is in the starring role]
9.
```sql
SELECT title FROM movie
JOIN casting ON movie.id = casting.movieid
JOIN actor ON actor.id = casting.actorid
WHERE casting.ord > 1 AND actor.name = 'Harrison Ford'
```
### List the films together with the leading star for all 1962 films.
10.
```sql
SELECT title, name FROM movie
JOIN casting ON movie.id = casting.movieid
JOIN actor ON actor.id = casting.actorid
WHERE casting.ord = 1 AND movie.yr = 1962
```

## NSS Tutorial

### Show the the percentage who STRONGLY AGREE
1.
```sql
SELECT A_STRONGLY_AGREE
  FROM nss
 WHERE question='Q01'
   AND institution='Edinburgh Napier University'
   AND subject='(8) Computer Science'
```
### Show the institution and subject where the score is at least 100 for question 15.
2.
```sql
SELECT institution, subject
  FROM nss
 WHERE question='Q15'
AND score >= 100
```
### Show the institution and score where the score for '(8) Computer Science' is less than 50 for question 'Q15'
3.
```sql
SELECT institution,score
  FROM nss
 WHERE question='Q15'
   AND score < 50
   AND subject='(8) Computer Science'
```
### Show the subject and total number of students who responded to question 22 for each of the subjects '(8) Computer Science' and '(H) Creative Arts and Design'.
4.
```sql
SELECT subject, SUM(response)
  FROM nss
 WHERE question='Q22'
   AND (subject='(H) Creative Arts and Design'
   OR subject='(8) Computer Science')
GROUP BY subject
```
### Show the subject and total number of students who A_STRONGLY_AGREE to question 22 for each of the subjects '(8) Computer Science' and '(H) Creative Arts and Design'.
5.
```sql
SELECT subject, SUM(response * A_STRONGLY_AGREE / 100)
  FROM nss
 WHERE question='Q22'
   AND (subject='(H) Creative Arts and Design'
   OR subject='(8) Computer Science')
GROUP BY subject
```
### Show the percentage of students who A_STRONGLY_AGREE to question 22 for the subject '(8) Computer Science' show the same figure for the subject '(H) Creative Arts and Design'.
6.
```sql
SELECT subject, ROUND(
SUM(response * A_STRONGLY_AGREE * 100) /
SUM(response * (A_STRONGLY_DISAGREE + A_DISAGREE + A_NEUTRAL + A_AGREE + A_STRONGLY_AGREE))
)
  FROM nss
 WHERE question='Q22'
   AND (subject='(H) Creative Arts and Design'
   OR subject='(8) Computer Science')
GROUP BY subject
```

## SELF JOIN

### How many stops are in the database.
1.
```sql
SELECT COUNT(*) FROM stops
```
### Find the id value for the stop 'Craiglockhart'
2.
```sql
SELECT stops.id FROM stops
WHERE name = 'Craiglockhart'
```
### Give the id and the name for the stops on the '4' 'LRT' service.
3.
```sql
SELECT id, name FROM stops
JOIN route ON stops.id = route.stop
WHERE num = 4 AND company = 'LRT'
```
### Routes and stops(1)
4.
The query shown gives the number of routes that visit either London Road (149) or Craiglockhart (53). Run the query and notice the two services that link these stops have a count of 2. Add a HAVING clause to restrict the output to these two routes.

```sql
SELECT company, num, COUNT(*)
FROM route WHERE stop=149 OR stop=53
GROUP BY company, num
HAVING COUNT(*) > 1
```
### Routes and stops(2)
5.
Execute the self join shown and observe that b.stop gives all the places you can get to from Craiglockhart, without changing routes. Change the query so that it shows the services from Craiglockhart to London Road.

```sql
SELECT a.company, a.num, a.stop, b.stop
FROM route a JOIN route b ON
  (a.company=b.company AND a.num=b.num)
WHERE a.stop=53 AND b.stop = (
SELECT id FROM stops
WHERE name = 'London Road'
)
```
### Routes and stops(3)
6.
The query shown is similar to the previous one, however by joining two copies of the stops table we can refer to stops by name rather than by number. Change the query so that the services between 'Craiglockhart' and 'London Road' are shown. If you are tired of these places try 'Fairmilehead' against 'Tollcross'

```sql
SELECT a.company, a.num, stopa.name, stopb.name
FROM route a JOIN route b ON
  (a.company=b.company AND a.num=b.num)
  JOIN stops stopa ON (a.stop=stopa.id)
  JOIN stops stopb ON (b.stop=stopb.id)
WHERE stopa.name='Craiglockhart' AND stopb.name = 'London Road'
```
### Using Self `JOIN`
7.
Give a list of all the services which connect stops 115 and 137 ('Haymarket' and 'Leith')

```sql
SELECT a.company, a.num
FROM route a JOIN route b ON
  (a.company=b.company AND a.num=b.num)
  JOIN stops stopa ON (a.stop=stopa.id)
  JOIN stops stopb ON (b.stop=stopb.id)
WHERE stopa.name='Haymarket' AND stopb.name = 'Leith'
GROUP BY company, num
```
### Working with self join
8.
Give a list of the services which connect the stops 'Craiglockhart' and 'Tollcross'

```sql
SELECT a.company, a.num
FROM route a JOIN route b ON
  (a.company=b.company AND a.num=b.num)
  JOIN stops stopa ON (a.stop=stopa.id)
  JOIN stops stopb ON (b.stop=stopb.id)
WHERE stopa.name='Craiglockhart' AND stopb.name = 'Tollcross'
GROUP BY company, num
```
### Using `JOIN` 
9.
Give a distinct list of the stops which may be reached from 'Craiglockhart' by taking one bus, including 'Craiglockhart' itself, offered by the LRT company. Include the company and bus no. of the relevant services.

```sql
SELECT stopb.name, a.company, a.num
FROM route a JOIN route b ON
(a.company=b.company AND a.num=b.num)
JOIN stops stopa ON stopa.id = a.stop
JOIN stops stopb ON stopb.id = b.stop
WHERE a.company = 'LRT' AND stopa.name = 'Craiglockhart'
GROUP BY company, num, name
ORDER BY stopb.name ASC
```

