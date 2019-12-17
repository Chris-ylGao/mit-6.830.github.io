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
9. ->
```ruby

```
10. ->
```ruby

```
1. ->
```ruby

```
1. ->
```ruby

```
