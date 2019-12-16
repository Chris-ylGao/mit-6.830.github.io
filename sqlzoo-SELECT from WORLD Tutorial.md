1. -> show the name, continent and population of all countries.
```ruby
SELECT name, continent, population 
FROM world;
```
2. -> Show the name for the countries that have a population of at least 200 million. 200 million is 200000000;
```ruby
SELECT name 
FROM world
WHERE population >= 200000000;
```
3. -> Give the name and the per capita GDP for those countries with a population of at least 200 million.
```ruby
SELECT name,gdp/population
FROM world
WHERE population >= 200000000;
```
4. -> Show the name and population in millions for the countries of the continent 'South America'. Divide the population by 1000000 to get population in millions.
```ruby
SELECT name , population/1000000
FROM world
WHERE continent='South America';
```
5. -> Show the name and population for France, Germany, Italy
```ruby
SELECT name, population
FROM world
WHERE name IN ('France', 'Germany', 'Italy');
```
6. -> Show the countries which have a name that includes the word 'United'
```ruby
SELECT name 
FROM world 
WHERE name LIKE '%United%';
```
7. -> Show the countries that are big by area or big by population. Show name, population and area.
```ruby
SELECT name, population, area
FROM world
WHERE area>3000000 OR population > 250000000;
```
8. ->  Show the countries that are big by area (more than 3 million) or big by population (more than 250 million) but not both. 
Show name, population and area.
```ruby
SELECT name, population, area
FROM world
WHERE area > 3000000 XOR population > 250000000;
```
9. -> Show the name and population in millions and the GDP in billions for the countries of the continent 'South America'.
Use the ROUND function to show the values to two decimal places.
```ruby
SELECT name, ROUND(population/1000000,2), ROUND(gdp/1000000000,2)
FROM world
WHERE continent = 'South America';
```
10. -> Show the name and per-capita GDP for those countries with a GDP of at least one trillion
Round this value to the nearest 1000.
```ruby
SELECT name, ROUND(gdp/population,-3)
FROM world
WHERE gdp>=1000000000000;
```
11. -> Show the name and capital where the name and the capital have the same number of characters.
```ruby
SELECT name, capital
FROM world 
WHERE LENGTH(name)=LENGTH(capital);
```
12. -> Show the name and the capital where the first letters of each match. 
Don't include countries where the name and the capital are the same word.
```ruby
SELECT name, capital 
FROM world
WHERE LEFT(name,1) = LEFT(capital,1) AND name <> capital;
```
13. -> Find the country that has all the vowels and no spaces in its name.
```ruby
SELECT name
FROM world
WHERE name LIKE '%a%
AND name LIKE '%e%'
AND name LIKE '%i%'
AND name LIKE '%o%'
AND name LIKE '%u%'
AND name NOT LIKE '% %';
```
