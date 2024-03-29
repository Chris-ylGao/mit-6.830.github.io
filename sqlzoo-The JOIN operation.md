1. -> show the matchid and player name for all goals scored by Germany. 
To identify German players, check for: teamid = 'GER'
```ruby
SELECT matchid, player FROM goal 
WHERE teamid = 'GER';
```
2. -> Show id, stadium, team1, team2 for just game 1012
```ruby
SELECT id,stadium,team1,team2
FROM game
WHERE ID =1012;
```
3. -> show the player, teamid, stadium and mdate for every German goal.
```ruby
SELECT player,teamid, stadium,mdate
FROM game JOIN goal ON (id=matchid)
WHERE teamid='GER';
```
4. -> Show the team1, team2 and player for every goal scored by a player called Mario player LIKE 'Mario%'
```ruby
SELECT team1, team2, player
FROM goal JOIN game ON (matchid = id)
WHERE player LIKE 'Mario%';
```
5. -> Show player, teamid, coach, gtime for all goals scored in the first 10 minutes gtime<=10
```ruby
SELECT player, teamid, coach,gtime
FROM goal JOIN eteam ON (teamid = id)
WHERE gtime<=10;
```
6. -> List the the dates of the matches and the name of the team in which 'Fernando Santos' was the team1 coach.
```ruby
SELECT mdate,teamname
FROM eteam JOIN game ON (team1=eteam.id)
WHERE coach =  'Fernando Santos';
```
7. -> List the player for every goal scored in a game where the stadium was 'National Stadium, Warsaw'
```ruby
SELECT player
FROM game JOIN goal ON (game.id = goal.matchid)
WHERE stadium = 'National Stadium, Warsaw';
```
8. -> Instead show the name of all players who scored a goal against Germany.
```ruby
SELECT DISTINCT player
 FROM game JOIN goal ON matchid = id 
WHERE (teamid = team1 AND team2 = 'GER')
OR (teamid = team2 AND team1 = 'GER')
```
9. -> Show teamname and the total number of goals scored.
```ruby
SELECT teamname, Count(matchid)
FROM eteam JOIN goal ON id=teamid
GROUP BY teamname
```
10. -> Show the stadium and the number of goals scored in each stadium.
```ruby
SELECT stadium, COUNT(*)
FROM game JOIN goal ON id = matchid
GROUP BY stadium
```
11. -> For every match involving 'POL', show the matchid, date and the number of goals scored.
```ruby
SELECT id, mdate, COUNT(*)
FROM game JOIN goal ON (id = matchid)
WHERE team1 = 'POL' OR team2 = 'POL' 
GROUP BY game.id, game.mdate;
```
12. -> For every match where 'GER' scored, show matchid, match date and the number of goals scored by 'GER'
```ruby
SELECT id, mdate, COUNT(*)
FROM game JOIN goal ON id = matchid
WHERE teamid = 'GER'
GROUP BY game.id,mdate;
```
13. -> List every match with the goals scored by each team as shown.
This will use "CASE WHEN" which has not been explained in any previous exercises.
```ruby
SELECT mdate,team1,
SUM(CASE WHEN teamid=team1 THEN 1 ELSE 0 END) score1,
team2,
SUM(CASE WHEN teamid=team2 THEN 1 ELSE 0 END) score2
FROM game JOIN goal ON matchid = id 
GROUP BY mdate,matchid,team1,team2;
```
