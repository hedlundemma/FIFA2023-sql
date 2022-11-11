<img src="https://media.giphy.com/media/SxFHr5dX6m0RYK21NY/giphy.gif">

# FIFA 2023 women’s world cup in football

We have created a great database with teams, players, stats and more!

Querys:

## // List all games today 
SELECT * 
FROM matches 
WHERE date = "2023-07-26";

//List a teams matches and results
SELECT * 
FROM matches 
WHERE home_team = 1 OR away_team=1;

//List a group table 
SELECT * 
FROM teams 
WHERE tournament_group = "A";

// List the top 10 players goal
SELECT * FROM players

INNER JOIN stats ON stats.player_id = players.id

WHERE "event" = "goal"

LIMIT 10

// List the top 10 players assist
SELECT * FROM players

INNER JOIN stats ON stats.player_id = players.id

WHERE "event" = "assist"

LIMIT 10


//Players that are unavailable due to disciplinary reasons
SELECT * 
FROM stats 
WHERE event = "red card" OR event = "yellow card"

ORDER BY event;

// List a teams roster 
SELECT "name", 
players.first_name as player_f_name, 
players.last_name as player_l_name, 
position, players.goals, 
matches_played,save_percentage, 
matches_started, 
minutes_played, 
coaches.first_name as coaches_f_name, 
coaches.last_name as coaches_l_name, 
shots_on_goal, 
"event" 
FROM teams

INNER JOIN players ON players.team_id = teams.id

INNER JOIN coaches ON teams.coaches_id = coaches.id

LEFT JOIN stats ON stats.player_id = players.id

LEFT JOIN shots ON shots.player_id = players.id

WHERE teams.id = 1;

// Detailed info about a finished game
SELECT team_id, 
home_team, 
away_team,
score_home_team, 
score_away_team, 
first_name, 
last_name, 
match_goals, 
cards, 
substitutions, 
referee_id, 
venues."name" AS venue_name, 
"date" 
FROM matches

INNER JOIN players ON matches.home_team = players.team_id OR matches.away_team = players.team_id

INNER JOIN venues ON matches.venue_id = venues.id

//Short info for the same game as above
SELECT "name", 
abbrevation, 
"flag", 
wins, 
draws, 
losses, 
points 
FROM teams

WHERE id IN (1,2);

// Playoff-tree 
SELECT name, 
teams.id AS team_id, 
home_team, 
away_team, 
abbrevation, 
"flag", 
"date", 
time, 
score_home_team, 
score_away_team, 
score_half_time 
FROM matches

INNER JOIN teams ON matches.home_team = teams.id OR matches.away_team = teams.id

WHERE type_of_game="RoS"


## Installation

1. Download the file fifa_2023.db
2. All information is in there so tell us what you want to know

## Thank you
