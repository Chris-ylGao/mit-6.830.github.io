1. -> List each country name where the population is larger than that of 'Russia'.
```ruby
SELECT name FROM world
 WHERE population > 
(SELECT population FROM world WHERE name='Russia')
```
2. -> Show the countries in Europe with a per capita GDP greater than 'United Kingdom'.
```ruby
SELECT name
FROM world
WHERE continent = 'Europe' 
AND gdp/population > 
(SELECT gdp/population FROM world WHERE name ='United Kingdom');
```
3. -> List the name and continent of countries in the continents containing either Argentina or Australia.
Order by name of the country.
```ruby
SELECT name, continent
FROM world
WHERE continent IN 
(SELECT continent FROM world WHERE name IN ('Argentina', 'Australia'))
ORDER BY name;
```
4. -> Which country has a population that is more than Canada but less than Poland? Show the name and the population.
```ruby
SELECT name, population
FROM world 
WHERE population > (SELECT population FROM world WHERE name = 'Canada')
AND population < (SELECT population FROM world WHERE name = 'Poland');
```
5. -> Show the name and the population of each country in Europe. 
Show the population as a percentage of the population of Germany.
```ruby
SELECT name, concat(ROUND(100* population/(SELECT population FROM world WHERE name='Germany'), 0), '%')
FROM world
WHERE continent='Europe';
```
6. -> Which countries have a GDP greater than every country in Europe? [Give the name only.]
```ruby
SELECT name 
FROM world
WHERE gdp > ALL(SELECT gdp FROM world WHERE continent ='Europe' AND gdp > 0);
```
7. -> Find the largest country (by area) in each continent, show the continent, the name and the area:
```ruby
SELECT continent, name, area
FROM world w1
WHERE area >= ALL(SELECT area FROM world w2 WHERE w1.continent = w2.continent AND w2.area >0);
```
8. -> List each continent and the name of the country that comes first alphabetically.
```ruby
SELECT continent, name
FROM world w1
WHERE name <= ALL(SELECT name FROM world w2 WHERE w1.continent = w2.continent);
```
9. -> Find the continents where all countries have a population <= 25000000. 
Then find the names of the countries associated with these continents. 
Show name, continent and population.
```ruby
SELECT name, continent,population
FROM world w1
WHERE continent IN 
(SELECT continent FROM world w2 WHERE 25000000 >= (SELECT MAX(population) FROM world w3 WHERE w2.continent = w3.continent));
```
10. -> Some countries have populations more than three times that of any of their neighbours (in the same continent).
Give the countries and continents.
```ruby
SELECT name,continent
FROM world w1
WHERE population > ALL(SELECT population*3 FROM world w2 WHERE w1.continent = w2.continent AND w1.name <>w2.name); 
```
