## teacher(id, dept, name.phone, mobile)
## dept(id, name)
1. -> List the teachers who have NULL for their department.
```ruby
SELECT name
FROM teacher 
WHERE dept IS NULL;
```
2. -> Note the INNER JOIN misses the teachers with no department and the departments with no teacher.
```ruby
SELECT teacher.name, dept.name
FROM teacher INNER JOIN dept ON (teacher.dept=dept.id)
```
3. -> Use a different JOIN so that all teachers are listed.
```ruby
SELECT teacher.name, dept.name
FROM teacher LEFT JOIN dept ON (teacher.dept=dept.id)
```
4. -> Use a different JOIN so that all departments are listed.
```ruby
SELECT teacher.name, dept.name
FROM teacher RIGHT JOIN dept
ON (teacher.dept=dept.id)
```
5. -> Show teacher name and mobile number or '07986 444 2266'
```ruby
SELECT name, COALESCE(mobile,  '07986 444 2266')
FROM teacher;
```
6. -> Use the COALESCE function and a LEFT JOIN to print the teacher name and department name. 
Use the string 'None' where there is no department.
```ruby
SELECT teacher.name, COALESCE(dept.name, 'None')
FROM teacher LEFT JOIN dept ON dept = dept.id;
```
7. -> Use COUNT to show the number of teachers and the number of mobile phones.
NOTE: COUNT() would not count the NULL value.
```ruby
SELECT COUNT(id), COUNT(mobile)
FROM teacher;
```
8. -> show each department and the number of staff
```ruby
SELECT dept.name, COUNT(teacher.id)
FROM teacher RIGHT JOIN dept ON dept = dept.id
GROUP BY dept.name;
```
9. -> Use CASE to show the name of each teacher followed by 'Sci' if the teacher is in dept 1 or 2 and 'Art' otherwise.
```ruby
SELECT name, 
CASE WHEN dept IN ('1', '2') THEN 'Sci' ELSE 'Art'  END
FROM teacher;
```
10. -> Use CASE to show the name of each teacher followed by 'Sci' if the teacher is in dept 1 or 2, show 'Art' if the teacher's dept is 3 and 'None' otherwise.
```ruby
SELECT name, 
CASE WHEN dept IN ('1', '2') THEN 'Sci' WHEN dept = 3 THEN 'Art' ELSE 'None'  END
FROM teacher;
```
