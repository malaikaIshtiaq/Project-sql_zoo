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
SELECT name, ROUND(gdp/population, -3) FROM world WHERE gdp > 100000000000;
```
