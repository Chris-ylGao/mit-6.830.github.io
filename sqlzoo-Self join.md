## stops(id, name)
## route(num, company, pos, stop)
1. -> How many stops are in the database.
```ruby
SELECT COUNT(*)
FROM stops;
```
2. -> Find the id value for the stop 'Craiglockhart'
```ruby
SELECT id 
FROM stops
WHERE name = 'Craiglockhart';
```
3. -> Give the id and the name for the stops on the '4' 'LRT' service.
```ruby
SELECT id,name FROM stops
WHERE id IN (SELECT stop FROM route WHERE num = 4 AND company = 'LRT');
```
4. ->The query shown gives the number of routes that visit either London Road (149) or Craiglockhart (53). 
Run the query and notice the two services that link these stops have a count of 2.
Add a HAVING clause to restrict the output to these two routes.
```ruby
SELECT company, num, COUNT(*)
FROM route WHERE stop=149 OR stop=53
GROUP BY company, num
HAVING COUNT(*) =2;
```
5. ->Execute the self join shown and observe that b.stop gives all the places you can get to from Craiglockhart, without changing routes. 
Change the query so that it shows the services from Craiglockhart to London Road.
```ruby
SELECT a.company, a.num, a.stop, b.stop
FROM route a JOIN route b ON
  (a.company=b.company AND a.num=b.num)
WHERE a.stop=53 AND b.stop =  149;
```
6. -> show the services between 'Craiglockhart' and 'London Road'
```ruby
SELECT a.company, a.num, stopa.name, stopb.name
FROM route a JOIN route b ON
  (a.company=b.company AND a.num=b.num)
  JOIN stops stopa ON (a.stop=stopa.id)
  JOIN stops stopb ON (b.stop=stopb.id)
WHERE stopa.name='Craiglockhart' AND stopb.name = 'London Road';
```
7. -> Give a list of all the services which connect stops 115 and 137 ('Haymarket' and 'Leith')
```ruby
SELECT DISTINCT r1.company, r1.num
FROM route r1 JOIN route r2 ON (r1.company = r2.company AND r1.num = r2.num)
WHERE r1.stop = 115 AND r2.stop = 137;
```
8. -> Give a list of the services which connect the stops 'Craiglockhart' and 'Tollcross'
```ruby
SELECT DISTINCT r1.company, r1.num
FROM route r1 JOIN route r2 ON (r1.company = r2.company AND r1.num = r2.num)
JOIN stops s1 ON (r1.stop = s1.id)
JOIN stops s2 ON (r2.stop = s2.id)
WHERE s1.name =  'Craiglockhart' AND s2.name =  'Tollcross';
```
9. ->Give a distinct list of the stops which may be reached from 'Craiglockhart' by taking one bus, including 'Craiglockhart' itself, offered by the LRT company.
Include the company and bus no. of the relevant services.
```ruby
SELECT s.name, r1.company,r1.num
FROM route r1 JOIN route r ON (r.company = r1.company AND r.num = r1.num)
JOIN stops s ON (r.stop = s.id) 
JOIN stops s1 ON (r1.stop = s1.id) 
WHERE s1.name = 'Craiglockhart' AND r1.company = 'LRT';
```
10. ->Find the routes involving two buses that can go from Craiglockhart to Lochend.
Show the bus no. and company for the first bus, the name of the stop for the transfer,
and the bus no. and company for the second bus.
```ruby
SELECT r1.num,  r1.company, s2.name, r3.num, r3.company
FROM route r1 JOIN route r2 ON (r1.company = r2.company AND r1.num = r2.num)
JOIN (route r3 JOIN route r4 ON (r3.company = r4.company AND r4.num = r3.num))
JOIN stops s1 ON (r1.stop = s1.id)
JOIN stops s2 ON (r2.stop = s2.id)
JOIN stops s3 ON (r3.stop = s3.id)
JOIN stops s4 ON (r4.stop = s4.id)
WHERE s1.name = 'Craiglockhart' AND s4.name = 'Lochend' AND s2.name = s3.name;
```
