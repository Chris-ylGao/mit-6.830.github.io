## movie(id, title, yr, director, budgey, gross)
## actor(id, name)
## casting (movieid, actorid, ord)
1. -> List the films where the yr is 1962 [Show id, title]
```ruby
SELECT id, title
FROM movie
WHERE yr=1962
```
2. -> When was Citizen Kane released?
```ruby
SELECT yr
FROM movie
WHERE title =  'Citizen Kane';
```
3. -> List all of the Star Trek movies, include the id, title and yr (all of these movies include the words Star Trek in the title).
      Order results by year.
```ruby
SELECT id, title,yr
FROM movie 
WHERE title LIKE '%Star Trek%'
ORDER BY yr;
```
4. -> What id number does the actor 'Glenn Close' have?
```ruby
SELECT id 
FROM actor
WHERE name = 'Glenn Close';
```
5. -> What is the id of the film 'Casablanca'
```ruby
SELECT id 
FROM movie
WHERE title = 'Casablanca';
```
6. -> Obtain the cast list for 'Casablanca'.
```ruby
SELECT name
FROM actor JOIN casting ON id = actorid
WHERE movieid =11768;
```
7. -> Obtain the cast list for the film 'Alien'
```ruby
SELECT name
FROM actor JOIN casting ON id = actorid
WHERE movieid = (SELECT id FROM movie WHERE title = 'Alien');
```
8. -> List the films in which 'Harrison Ford' has appeared
```ruby
SELECT title 
FROM movie JOIN casting ON id = movieid
WHERE actorid = (SELECT id FROM actor WHERE name =  'Harrison Ford');
```
9. -> List the films where 'Harrison Ford' has appeared - but not in the starring role. 
[Note: the ord field of casting gives the position of the actor. If ord=1 then this actor is in the starring role]
```ruby
SELECT title 
FROM movie JOIN casting ON id = movieid
WHERE ord <> 1
AND actorid = (SELECT id FROM actor WHERE name =  'Harrison Ford');
```
10. -> List the films together with the leading star for all 1962 films.
```ruby
SELECT title, name
FROM movie JOIN casting ON movie.id = movieid
           JOIN actor ON actorid = actor.id)
WHERE yr =  1962 
AND movieid = movie.id
AND actor.id = actorid 
AND ord = 1; 
```
11. -> show the year and the number of movies he made each year for any year in which he made more than 2 movies.
```ruby
SELECT yr,COUNT(title) 
FROM movie JOIN casting ON movie.id=movieid
           JOIN actor ON actorid=actor.id
WHERE name='Rock Hudson'
GROUP BY yr
HAVING COUNT(title) > 2
```
12. -> List the film title and the leading actor for all of the films 'Julie Andrews' played in.
```ruby
SELECT title, name
FROM movie JOIN casting ON movie.id = movieid
JOIN actor ON actor.id = actorid
WHERE movie.id = movieid
AND actor.id = actorid
AND ord = 1
AND movie.id IN (SELECT movieid FROM casting JOIN actor ON actorid = actor.id WHERE name = 'Julie Andrews');
```
13. -> Obtain a list, in alphabetical order, of actors who've had at least 30 starring roles.
```ruby
SELECT name
FROM actor JOIN casting ON actor.id = actorid
WHERE ord = 1
GROUP BY name
HAVING (COUNT(movieid) >= 30)
ORDER BY name;
```
14. -> List the films released in the year 1978 ordered by the number of actors in the cast, then by title.
```ruby
SELECT title, COUNT(actorid)
FROM movie JOIN casting ON movie.id = movieid
WHERE yr = 1978
AND movie.id = movieid
GROUP BY (movie.title)
ORDER BY COUNT(actorid) DESC, title;
```
15. -> List all the people who have worked with 'Art Garfunkel'.
```ruby
SELECT name 
FROM actor JOIN casting ON id = actorid 
WHERE movieid IN
(SELECT movieid FROM  casting JOIN actor ON (actorid = actorid AND name = 'Art Garfunkel'))
AND actor.name != 'Art Garfunkel'
GROUP BY name;
```
