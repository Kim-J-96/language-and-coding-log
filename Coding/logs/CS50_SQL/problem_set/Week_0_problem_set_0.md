# 🗃️ 2025-06-10 ~ 12 SQL Learning Log

## 📘 Today's Learning Content
- CS50’s Introduction to Databases with SQL 
  - WEEK 0 Problem Set 0 - Cyberchase / 36 Views / Normals / Players

## 🧪 Practice Examples - WEEK O Problem Set 0 - Cyberchase
- write a SQL query to list the titles of all episodes in Cyberchase’s original season, Season 1.
```sql
SELECT "title" FROM "episodes" 
WHERE "season" = 1;
```

- list the season number of, and title of, the first episode of every season.
```sql
SELECT "season", "title" FROM "episodes" 
WHERE "episode_in_season" = 1;
```

- find the production code for the episode “Hackerized!”.
```sql
SELECT "production_code" FROM "episodes" 
WHERE "title" = 'Hackerized!';
```

- write a query to find the titles of episodes that do not yet have a listed topic.
```sql
SELECT "title" FROM "episodes" 
WHERE "topic" IS NULL;
```

- find the title of the holiday episode that aired on December 31st, 2004.
```sql
SELECT "title" FROM "episodes" 
WHERE "air_date" = '2004-12-31';
```

- list the titles of episodes from season 6 (2008) that were released early, in 2007.
```sql
SELECT "title" FROM "episodes" 
WHERE "season" = 6 AND "air_date" LIKE "2007%";
```

- write a SQL query to list the titles and topics of all episodes teaching fractions.
```sql
SELECT "title", "topic" FROM "episodes" 
WHERE "topic" LIKE "%fractions%";
```

- write a query that counts the number of episodes released in the last 6 years, from 2018 to 2023, inclusive. You might find it helpful to know you can use BETWEEN with dates, such as BETWEEN '2000-01-01' AND '2000-12-31'.
```sql
SELECT COUNT("episode") FROM "episodes" 
WHERE "air_date" BETWEEN '2018-01-01' AND '2023-12-31';
```

- write a query that counts the number of episodes released in Cyberchase’s first 6 years, from 2002 to 2007, inclusive.
```sql
SELECT COUNT("episode") FROM "episodes" 
WHERE "air_date" BETWEEN '2002-01-01' AND '2007-12-31';
```

- write a SQL query to list the ids, titles, and production codes of all episodes. Order the results by production code, from earliest to latest.
```sql
SELECT "id", "title", "production_code" FROM "episodes" 
ORDER BY "production_code";
```

- list the titles of episodes from season 5, in reverse alphabetical order.
```sql
SELECT "title" FROM "episodes" 
WHERE "season" = 5 
ORDER BY "title" DESC;
```

- count the number of unique episode titles.
```sql
SELECT COUNT(DISTINCT "title") FROM "episodes";
```

- Write a SQL query to find the titles of episodes that have aired during the holiday season, usually in December in the United States.
```sql
SELECT "title", "air_date" FROM "episodes"
WHERE "air_date" LIKE "20__-12-__";
```

- Write a SQL query to find, for each year, the first day of the year that PBS released a Cyberchase episode.
  ❓have no idea yet

## 🧪 Practice Examples - WEEK O Problem Set 0 - 36 Views
- write a SQL query that a translator might take interest in: list, side by side, the Japanese title and the English title for each print Ensure the Japanese title is the first column, followed by the English title.
```sql
SELECT "japanese_title" AS "Japanese title", "english_title" AS "English title"
FROM "views";
```

- write a SQL query to list the average colors of prints by Hokusai that include “river” in the English title. (As an aside, do they have any hint of blue?)
```sql
SELECT "average_color" FROM "views"
WHERE "artist" = 'Hokusai' AND "english_title" LIKE "%river%";
```

- write a SQL query to count how many prints by Hokusai include “Fuji” in the English title. Though all of Hokusai’s prints focused on Mt. Fuji, in how many did “Fuji” make it into the title?
```sql
SELECT COUNT("english_title") FROM "views"
WHERE "english_title" LIKE "% Fuji %";
```
** “Fuji” NOT  “Mt.Fuji”

- write a SQL query to count how many prints by Hiroshige have English titles that refer to the “Eastern Capital”. Hiroshige’s prints were created in Japan’s “Edo period,” referencing the eastern capital city of Edo, now Tokyo.
```sql
SELECT COUNT("english_title") FROM "views"
WHERE "artist" = 'Hiroshige'
AND "english_title" LIKE "%Eastern Capital%";
```

- write a SQL query to find the highest contrast value of prints by Hokusai. Name the column “Maximum Contrast”. Does Hokusai’s prints most contrasting print actually have much contrast?
```sql
SELECT MAX("contrast") AS "Maximum contrast" FROM "views"
WHERE "artist" = 'Hokusai';
```

- write a SQL query to find the average entropy of prints by Hiroshige, rounded to two decimal places. Call the resulting column “Hiroshige Average Entropy”.
```sql
SELECT ROUND(AVG("entropy"), 2) AS "Hiroshige Average Entropy" FROM "views"
WHERE "artist" = 'Hiroshige';
```

- write a SQL query to list the English titles of the 5 brightest prints by Hiroshige, from most to least bright. Compare them to this list on Wikipedia to see if your results match the print’s aesthetics.
```sql
SELECT "english_title" AS "English title" FROM "views"
WHERE "artist" = 'Hiroshige'
ORDER BY "brightness" DESC
LIMIT 5;
```
** 🔥 LIMIT always comes at the end, like the cherry on top 🍒

- write a SQL query to list the English titles of the 5 prints with the least contrast by Hokusai, from least to highest contrast. Compare them to this list on Wikipedia to see if your results match the print’s aesthetics.
```sql
SELECT "english_title" FROM "views"
WHERE "artist" = 'Hokusai'
ORDER BY "contrast" ASC
LIMIT 5;
```
** ❗️from least to highest contrast❗️

- write a SQL query to find the English title and artist of the print with the highest brightness.
```sql
SELECT "english_title" AS "English title", "artist" FROM "views"
ORDER BY "brightness" DESC
LIMIT 1;
```

- write a SQL query to answer a question of your choice about the prints. The query should:
Make use of AS to rename a column
Involve at least one condition, using WHERE
Sort by at least one column, using ORDER BY

  - Write a SQL query to list the English titles and brightness values of all prints by Hokusai that have a brightness greater than 0.5. Rename the english_title column to print_title and the brightness column to light_level. Sort the results by light_level from brightest to darkest.
```sql
SELECT "english_title" AS "print_title", "brightness" AS "light_level" FROM "views"
WHERE "artist" = 'Hokusai' AND "brightness" > 0.5
ORDER BY "brightness" DESC;
```

## 🧪 Practice Examples - WEEK O Problem Set 0 - Normals
- write a SQL query to find the normal ocean surface temperature in the Gulf of Maine, off the coast of Massachusetts. To find this temperature, look at the data associated with 42.5° of latitude and -69.5° of longitude.
Recall that you can find the normal ocean surface temperature in the 0m column, which stands for 0 meters of depth!
```sql
SELECT "0m" FROM "normals"
WHERE "latitude" = '42.5' AND "longitude" = '-69.5';
```

- write a SQL query to find the normal temperature of the deepest sensor near the Gulf of Maine, at the same coordinate above.
The deepest sensor records temperatures at 225 meters of depth, so you can find this data in the 225m column.
```sql
SELECT "225m" FROM "normals"
WHERE "latitude" = '42.5' AND "longitude" = '-69.5';
```

- choose a location of your own and write a SQL query to find the normal temperature at 0 meters, 100 meters, and 200 meters. You might find Google Earth helpful if you’d like to find some coordinates to use!
```sql
SELECT "0m", "100m", "200m" FROM "normals"
WHERE "latitude" = '42.5' AND "longitude" = '-69.5';
```

- write a SQL query to find the lowest normal ocean surface temperature.
```sql
SELECT MIN("0m") FROM "normals";
```

- write a SQL query to find the highest normal ocean surface temperature.
```sql
SELECT MAX("0m") FROM "normals";
```

- write a SQL query to return all normal ocean temperatures at 50m of depth, as well as their respective degrees of latitude and longitude, within the Arabian Sea. Include latitude, longitude, and temperature columns. For simplicity, assume the Arabian Sea is encased in the following four coordinates:
20° of latitude, 55° of longitude
20° of latitude, 75° of longitude
0° of latitude, 55° degrees of longitude
0° of latitude, 75° degrees of longitude
```sql
SELECT "latitude", "longitude", "50m" FROM "normals"
WHERE ("latitude" BETWEEN 0 AND 20)
AND ("longitude" BETWEEN 55 AND 75);
```

- write a SQL query to find the average ocean surface temperature, rounded to two decimal places, along the equator. Call the resulting column “Average Equator Ocean Surface Temperature”.
The equator’s ocean surface temperatures can be found at all longitudes between the latitudes -0.5° and 0.5°, inclusive.
```sql
SELECT ROUND(AVG("0m"), 2) AS "Average Equator Ocean Surface Temperature" FROM "normals"
WHERE "latitude" BETWEEN -0.5 AND 0.5;
```

- write a SQL query to find the 10 locations with the lowest normal ocean surface temperature, sorted coldest to warmest. If two locations have the same normal ocean surface temperature, sort by latitude, smallest to largest. Include latitude, longitude, and surface temperature columns.
```sql
SELECT "latitude", "longitude", "0m" AS "surface temperature" FROM "normals"
ORDER BY "0m", "latitude"
LIMIT 10;
```
- write a SQL query to find the 10 locations with the highest normal ocean surface temperature, sorted warmest to coldest. If two locations have the same normal ocean surface temperature, sort by latitude, smallest to largest. Include latitude, longitude, and surface temperature columns.
There are 180 whole degrees of latitude. 
```sql
SELECT "latitude", "longitude", "0m" AS "surface temperature" FROM "normals"
ORDER BY "0m" DESC, "latitude"
LIMIT 10;
```

- write a SQL query to determine how many points of latitude we have at least one data point for. (Why might we not have data points for all latitudes?)
```sql
SELECT COUNT(DISTINCT ROUND("latitude")) FROM "normals"
WHERE "latitude" IS NOT NULL;
```

## 🧪 Practice Examples - WEEK O Problem Set 0 - Players
- write a SQL query to find the hometown (including city, state, and country) of Jackie Robinson.
```sql
SELECT "birth_city", "birth_state", "birth_country" FROM "players"
WHERE "first_name" = 'Jackie' AND "last_name" = 'Robinson';
```

- write a SQL query to find the side (e.g., right or left) Babe Ruth hit.
```sql
SELECT "bats" FROM "players"
WHERE "first_name" = 'Babe' AND "last_name" = 'Ruth';
```

- write a SQL query to find the ids of rows for which a value in the column debut is missing.
```sql
SELECT "id" FROM "players"
WHERE "debut" IS NULL;
```

- write a SQL query to find the first and last names of players who were not born in the United States. Sort the results alphabetically by first name, then by last name.
```sql
SELECT "first_name", "last_name" FROM "players"
WHERE NOT "birth_country" = 'USA'
ORDER BY "first_name", "last_name";
```

- write a SQL query to return the first and last names of all right-handed batters. Sort the results alphabetically by first name, then by last name.
```sql
SELECT "first_name", "last_name" FROM "players"
WHERE "bats" = 'R'
ORDER BY "first_name", "last_name" ASC;
```

- write a SQL query to return the first name, last name, and debut date of players born in Pittsburgh, Pennsylvania (PA). Sort the results first by debut date—from most recent to oldest—then alphabetically by first name, followed by last name.
```sql
SELECT "first_name", "last_name", "debut" FROM "players"
WHERE "birth_state" = 'PA' AND "birth_city" = 'Pittsburgh'
ORDER BY "debut" DESC, "first_name", "last_name" ASC;
```

- write a SQL query to count the number of players who bat (or batted) right-handed and throw (or threw) left-handed, or vice versa.
```sql
SELECT COUNT(*) AS "players_count" FROM "players"
WHERE "bats" = 'R' AND "throws" = 'L' OR "bats" = 'L' AND "throws" = 'R';
```

- write a SQL query to find the average height and weight, rounded to two decimal places, of baseball players who debuted on or after January 1st, 2000. Return the columns with the name “Average Height” and “Average Weight”, respectively.
```sql
SELECT ROUND(AVG("height"), 2) AS "Average Height",
       ROUND(AVG("weight"), 2) AS "Average Weight"
FROM "players"
WHERE "debut" >= '2000-01-01';
```

- write a SQL query to find the players who played their final game in the MLB in 2022. Sort the results alphabetically by first name, then by last name.
```sql
SELECT "first_name", "last_name" FROM "players"
WHERE "final_game" LIKE "2022%"
ORDER BY "first_name", "last_name";
```

- Write a single SQL query to list the first and last names of all players of above average height, sorted tallest to shortest, then by first and last name.
Make use of AS to rename a column
Involve at least condition, using WHERE
Sort by at least one column using ORDER BY
```sql
SELECT "first_name" AS "FN", "last_name" AS "LN", "height" FROM "players"
WHERE "height" > (SELECT AVG("height") FROM "players")
ORDER BY "height" DESC, "first_name", "last_name";
```

## 🎯 Plan for next step
- CS50’s Introduction to Databases with SQL
  - WEEK 0 - 36 Views / Normals / Players
- Review WEEK 0