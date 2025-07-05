# 🗃️ 2025-06-28 ～ 2025-07-05 SQL Learning Log

## 📘 Today's Learning Content
- CS50’s Introduction to Databases with SQL 
  - WEEK 0 Problem Set 1 - Packages, Please / DESE / Moneyball

## 🧪 Practice Examples - WEEK 1 Problem Set 1 - Packages, Please

-- *** The Lost Letter ***
  - At what type of address did the Lost Letter end up?: Residential
  - At what address did the Lost Letter end up?: 2 Finnigan Street

```sql
SELECT "address" FROM "addresses"
WHERE "address" LIKE '%2 F% Street';

SELECT "type" FROM "addresses"
WHERE "address" = '2 Finnigan Street';

SELECT "contents" FROM "packages"
WHERE "id" = (
    SELECT "package_id" FROM "scans"
    WHERE "address_id" = (
        SELECT "id" FROM "addresses"
        WHERE "address" = '2 Finnigan Street'
    )
);

SELECT "address" FROM "addresses"
WHERE "id" = (
    SELECT "to_address_id" FROM "packages"
    WHERE "contents" = 'Congratulatory letter'
);

```
-- *** The Devious Delivery ***
   - At what type of address did the Devious Delivery end up?: Police Station
   - What were the contents of the Devious Delivery?: Duck debugger

```sql
SELECT "contents" FROM "packages"
WHERE "from_address_id" IS NULL;

SELECT "action" FROM "scans"
WHERE "package_id" = (
    SELECT "id" FROM "packages"
    WHERE "contents" = 'Duck debugger'
);

SELECT "type" FROM "addresses"
WHERE "id" = (
     SELECT "address_id" FROM "scans"
     WHERE "package_id" = (
         SELECT "id" FROM "packages"
         WHERE "contents" = 'Duck debugger' AND "action" = "Drop"
    )
);
```

-- *** The Forgotten Gift ***
   - What are the contents of the Forgotten Gift?: Flowers
   - Who has the Forgotten Gift?: Mikel

```sql
SELECT "contents" FROM "packages"
WHERE "from_address_id" = (
    SELECT "id" FROM "addresses"
    WHERE "address" = '109 Tileston Street'
);

SELECT "name" FROM "drivers"
WHERE "id" = (
    SELECT "driver_id" FROM "scans"
    WHERE "timestamp" = (
        SELECT "timestamp" FROM "scans"
        WHERE "package_id" = (
            SELECT "id" FROM "packages"
            WHERE "contents" = 'Flowers'
        )
        ORDER BY "timestamp" DESC
        LIMIT 1
    )
);
```

## 🧪 Practice Examples - WEEK 1 Problem Set 1 - DESE
- Your colleague is preparing a map of all public schools in Massachusetts. In 1.sql, write a SQL query to find the names and cities of all public schools in Massachusetts.

   - Keep in mind that not all schools in the schools table are considered traditional public schools. Massachusetts also recognizes charter schools, which (according to DESE!) are considered distinct.
```sql
SELECT "name", "city" FROM "schools"
WHERE "type" = 'Public School';
```

- Your team is working on archiving old data. In 2.sql, write a SQL query to find the names of districts that are no longer operational.

   - Districts that are no longer operational have “(non-op)” at the end of their name.
```sql
SELECT "name" FROM "districts"
WHERE "name" LIKE '%(non-op)';
```

- The Massachusetts Legislature would like to learn how much money, on average, districts spent per-pupil last year. In 3.sql, write a SQL query to find the average per-pupil expenditure. Name the column “Average District Per-Pupil Expenditure”.

   - Note the per_pupil_expenditure column in the expenditures table contains the average amount, per pupil, each district spent last year. You’ve been asked to find the average of this set of averages, weighting all districts equally regardless of their size.
```sql
SELECT AVG("per_pupil_expenditure") AS "Average District Per-Pupil Expenditure" FROM "expenditures";
```

- Some cities have more public schools than others. In 4.sql, write a SQL query to find the 10 cities with the most public schools. Your query should return the names of the cities and the number of public schools within them, ordered from greatest number of public schools to least. If two cities have the same number of public schools, order them alphabetically.
```sql
SELECT "city", COUNT("name") AS "number of public schools" FROM "schools"
WHERE "type" = 'Public School'
GROUP BY city
ORDER BY "number of public schools" DESC, "city" ASC
LIMIT 10;
```

- DESE would like you to determine in what cities additional public schools might be needed. In 5.sql, write a SQL query to find cities with 3 or fewer public schools. Your query should return the names of the cities and the number of public schools within them, ordered from greatest number of public schools to least. If two cities have the same number of public schools, order them alphabetically.
```sql
SELECT "city", COUNT("name") AS "number of public schools" FROM "schools"
WHERE "type" = 'Public School'
GROUP BY city
HAVING "number of public schools" <= 3
ORDER BY "number of public schools" DESC, "city" ASC;
```

- DESE wants to assess which schools achieved a 100% graduation rate. In 6.sql, write a SQL query to find the names of schools (public or charter!) that reported a 100% graduation rate.
```sql
SELECT "name" FROM "schools"
WHERE "id" IN (
    SELECT "school_id" FROM "graduation_rates"
    WHERE "graduated" = 100
);
```

- DESE is preparing a report on schools in the Cambridge school district. In 7.sql, write a SQL query to find the names of schools (public or charter!) in the Cambridge school district. Keep in mind that Cambridge, the city, contains a few school districts, but DESE is interested in the district whose name is “Cambridge.”
```sql
SELECT "name" FROM "schools"
WHERE "district_id" IN (
    SELECT "id" FROM "districts"
    WHERE "name" = 'Cambridge'
);
```

- A parent wants to send their child to a district with many other students. In 8.sql, write a SQL query to display the names of all school districts and the number of pupils enrolled in each.
```sql
SELECT "name", "pupils" FROM (
    SELECT * FROM "expenditures"
    LEFT JOIN "districts" ON "districts"."id" = "expenditures"."district_id"
);
```

- Another parent wants to send their child to a district with few other students. In 9.sql, write a SQL query to find the name (or names) of the school district(s) with the single least number of pupils. Report only the name(s).
```sql
SELECT "name" FROM (
    SELECT * FROM "districts"
    LEFT JOIN "expenditures" ON "expenditures"."district_id" = "districts"."id"
)
WHERE "pupils" = (
    SELECT MIN("pupils") FROM "expenditures"
);
```

- In Massachusetts, school district expenditures are in part determined by local taxes on property (e.g., home) values. In 10.sql, write a SQL query to find the 10 public school districts with the highest per-pupil expenditures. Your query should return the names of the districts and the per-pupil expenditure for each.
```sql
SELECT "name", "per_pupil_expenditure" FROM (
    SELECT * FROM "districts"
    LEFT JOIN "expenditures" ON "expenditures"."district_id" = "districts"."id"
)
WHERE "type" = "Public School District"
ORDER BY "per_pupil_expenditure" DESC
LIMIT 10;
```

- Is there a relationship between school expenditures and graduation rates? In 11.sql, write a SQL query to display the names of schools, their per-pupil expenditure, and their graduation rate. Sort the schools from greatest per-pupil expenditure to least. If two schools have the same per-pupil expenditure, sort by school name.

   - You should assume a school spends the same amount per-pupil their district as a whole spends.
```sql
SELECT "name", "per_pupil_expenditure", "graduated" FROM (
    SELECT * FROM "schools"
    JOIN "expenditures" ON "schools"."district_id" = "expenditures"."district_id"
    JOIN "graduation_rates" ON "schools"."id" = "graduation_rates"."school_id"
)
ORDER BY "per_pupil_expenditure" DESC, "name" ASC;
```

- A parent asks you for advice on finding the best public school districts in Massachusetts. In 12.sql, write a SQL query to find public school districts with above-average per-pupil expenditures and an above-average percentage of teachers rated “exemplary”. Your query should return the districts’ names, along with their per-pupil expenditures and percentage of teachers rated exemplary. Sort the results first by the percentage of teachers rated exemplary (high to low), then by the per-pupil expenditure (high to low).
```sql
SELECT "exemplary", "per_pupil_expenditure", "name" FROM (
    SELECT * FROM "districts"
    LEFT JOIN "expenditures" ON "districts"."id" = "expenditures"."district_id"
    LEFT JOIN "staff_evaluations" ON "expenditures"."district_id" = "staff_evaluations"."district_id"
)
WHERE "per_pupil_expenditure" > (
    SELECT AVG("per_pupil_expenditure") FROM "expenditures"
) AND "exemplary" > (
    SELECT AVG("exemplary") FROM "staff_evaluations"
)
AND "type" = "Public School District"
ORDER BY "exemplary" DESC, "per_pupil_expenditure" DESC;
```

- In 13.sql, write a SQL query to answer a question you have about the data! The query should:

   - Involve at least one JOIN or subquery
   - 教师满意度前10的学校和所在地区
```sql
SELECT "exemplary", "name" FROM (
    SELECT * FROM "staff_evaluations"
    LEFT JOIN "schools" ON "staff_evaluations"."district_id" = "schools"."district_id"
)
ORDER BY "exemplary" DESC, "name" ASC
LIMIT 10;
```

## 🧪 Practice Examples - WEEK 1 Problem Set 1 - Moneyball
- You should start by getting a sense for how average player salaries have changed over time. In 1.sql, write a SQL query to find the average player salary by year.

  - Sort by year in descending order.
  - Round the salary to two decimal places and call the column “average salary”.
  - Your query should return a table with two columns, one for year and one for average salary.
```sql
SELECT ROUND(AVG("salary"), 2) AS "average salary", "year"
FROM "salaries"
GROUP BY "year"
ORDER BY "year" DESC;
```

- Your general manager (i.e., the person who makes decisions about player contracts) asks you whether the team should trade a current player for Cal Ripken Jr., a star player who’s likely nearing his retirement. In 2.sql, write a SQL query to find Cal Ripken Jr.’s salary history.

   - Sort by year in descending order.
   - Your query should return a table with two columns, one for year and one for salary.
```sql
SELECT "salary", "year" FROM (
    SELECT * FROM "salaries"
    LEFT JOIN "players" ON "salaries"."player_id" = "players"."id"
)
WHERE "first_name" = 'Cal' AND "last_name" = 'Ripken'
ORDER BY "year" DESC;
```

- Your team is going to need a great home run hitter. Ken Griffey Jr., a long-time Silver Slugger and Gold Glove award winner, might be a good prospect. In 3.sql, write a SQL query to find Ken Griffey Jr.’s home run history.

   - Sort by year in descending order.
   - Note that there may be two players with the name “Ken Griffey.” This Ken Griffey was born in 1969.
   - Your query should return a table with two columns, one for year and one for home runs.
```sql
SELECT "year", "HR" FROM (
    SELECT * FROM "performances"
    LEFT JOIN "players" ON "performances"."player_id" = "players"."id"
)
WHERE "first_name" = 'Ken' AND "last_name" = 'Griffey' AND "birth_year" = 1969
ORDER BY "year" DESC;
```

- You need to make a recommendation about which players the team should consider hiring. With the team’s dwindling budget, the general manager wants to know which players were paid the lowest salaries in 2001. In 4.sql, write a SQL query to find the 50 players paid the least in 2001.

   - Sort players by salary, lowest to highest.
   - If two players have the same salary, sort alphabetically by first name and then by last name.
   - If two players have the same first and last name, sort by player ID.
   - Your query should return three columns, one for players’ first names, one for their last names, and one for their salaries.
```sql
SELECT "first_name", "last_name", "salary" FROM (
    SELECT * FROM "players"
    LEFT JOIN "salaries" ON "players"."id" = "salaries"."player_id"
)
WHERE "year" = 2001
ORDER BY "salary", "first_name", "last_name", "player_id"
LIMIT 50;
```

- It’s a bit of a slow day in the office. Though Satchel no longer plays, in 5.sql, write a SQL query to find all teams that Satchel Paige played for.

   - Your query should return a table with a single column, one for the name of the teams
```sql
SELECT "name" FROM (
    SELECT * FROM "players"
    LEFT JOIN "performances" ON "players"."id" = "performances"."player_id"
    LEFT JOIN "teams" ON "performances"."team_id" = "teams"."id"
)
WHERE "first_name" = 'Satchel' AND "last_name" = 'Paige'
GROUP BY "name";
```

- Which teams might be the biggest competition for the A’s this year? In 6.sql, wite a SQL query to return the top 5 teams, sorted by the total number of hits by players in 2001.

   - Call the column representing total hits by players in 2001 “total hits”.
   - Sort by total hits, highest to lowest.
   - Your query should return two columns, one for the teams’ names and one for their total hits in 2001.
```sql
SELECT "name", SUM("H") AS "total hits" FROM (
    SELECT * FROM "performances"
    LEFT JOIN "teams" ON "teams"."id" = "performances"."team_id"
    LEFT JOIN "players" ON "performances"."player_id" = "players"."id"
)
WHERE "year" = 2001
GROUP BY "name"
ORDER BY "total hits" DESC
LIMIT 5;
```

- You need to make a recommendation about which player (or players) to avoid recruiting. In 7.sql, write a SQL query to find the name of the player who’s been paid the highest salary, of all time, in Major League Baseball.

   - Your query should return a table with two columns, one for the player’s first name and one for their last name.
```sql
SELECT "first_name", "last_name" FROM (
    SELECT * FROM "players"
    LEFT JOIN "salaries" ON "players"."id" = "salaries"."player_id"
)
WHERE "salary" = (
    SELECT MAX("salary") FROM "salaries"
);
```

- How much would the A’s need to pay to get the best home run hitter this past season? In 8.sql, write a SQL query to find the 2001 salary of the player who hit the most home runs in 2001.

   - Your query should return a table with one column, the salary of the player.
```sql
SELECT "salary" FROM (
    SELECT * FROM "salaries"
    LEFT JOIN "performances" ON "salaries"."player_id" = "performances"."player_id"
)
WHERE "year" = 2001 AND "HR" = (
  SELECT MAX("HR") FROM "performances"
  WHERE "year" = 2001
);
```

- What salaries are other teams paying? In 9.sql, write a SQL query to find the 5 lowest paying teams (by average salary) in 2001.

   - Round the average salary column to two decimal places and call it “average salary”.
   - Sort the teams by average salary, least to greatest.
   - Your query should return a table with two columns, one for the teams’ names and one for their average salary.
```sql
SELECT "name", ROUND(AVG("salary"), 2) AS "average salary" FROM (
    SELECT * FROM "salaries"
    JOIN "teams" ON "salaries"."team_id" = "teams"."id"
)
WHERE "year" = 2001
GROUP BY "name"
ORDER BY "average salary"
LIMIT 5;

SELECT "name", ROUND(AVG("salary"), 2) AS "average salary" FROM (
    SELECT "salaries"."year", "salaries"."salary", "teams"."id", "teams"."name" FROM "salaries"
    JOIN "teams" ON "salaries"."team_id" = "teams"."id"
)
WHERE "year" = 2001
GROUP BY "name"
ORDER BY "average salary"
LIMIT 5;
```

- The general manager has asked you for a report which details each player’s name, their salary for each year they’ve been playing, and their number of home runs for each year they’ve been playing. To be precise, the table should include:

   - All player’s first names
   - All player’s last names
   - All player’s salaries
   - All player’s home runs
   - The year in which the player was paid that salary and hit those home runs
 - In 10.sql, write a query to return just such a table.
  
   - Your query should return a table with five columns, per the above.
   - Order the results, first and foremost, by player’s IDs (least to greatest).
   - Order rows about the same player by year, in descending order.
   - Consider a corner case: suppose a player has multiple salaries or performances for a given year. Order them first by number of home runs, in descending order, followed by salary, in descending order.
   - Be careful to ensure that, for a single row, the salary’s year and the performance’s year match.
```sql
SELECT "first_name", "last_name", "salary", "HR", "year" FROM (
    SELECT * FROM "players"
    JOIN "salaries" ON "players"."id" = "salaries"."player_id"
    JOIN "performances" ON "salaries"."player_id" = "performances"."player_id"
    AND "salaries"."year" = "performances"."year"
)
ORDER BY "player_id", "year" DESC, "HR" DESC, "salary" DESC;
```

- You need a player that can get hits. Who might be the most underrated? In 11.sql, write a SQL query to find the 10 least expensive players per hit in 2001.

   - Your query should return a table with three columns, one for the players’ first names, one of their last names, and one called “dollars per hit”.
   - You can calculate the “dollars per hit” column by dividing a player’s 2001 salary by the number of hits they made in 2001. Recall you can use AS to rename a column.
   - Dividing a salary by 0 hits will result in a NULL value. Avoid the issue by filtering out players with 0 hits.
   - Sort the table by the “dollars per hit” column, least to most expensive. If two players have the same “dollars per hit”, order by first name, followed by last name, in alphabetical order.
   - As in 10.sql, ensure that the salary’s year and the performance’s year match.
   - You may assume, for simplicity, that a player will only have one salary and one performance in 2001.
```sql
SELECT "first_name", "last_name", "salary" / "H" AS "dollars per hit" FROM (
    SELECT * FROM "players"
    JOIN "salaries" ON "players"."id" = "salaries"."player_id"
    JOIN "performances" ON "salaries"."player_id" = "performances"."player_id"
    AND "salaries"."year" = "performances"."year"
)
WHERE "H" != 0 AND "year" = 2001
ORDER BY "dollars per hit", "first_name", "last_name"
LIMIT 10;
```

- Hits are great, but so are RBIs! In 12.sql, write a SQL query to find the players among the 10 least expensive players per hit and among the 10 least expensive players per RBI in 2001.

   - Your query should return a table with two columns, one for the players’ first names and one of their last names.
   - You can calculate a player’s salary per RBI by dividing their 2001 salary by their number of RBIs in 2001.
   - You may assume, for simplicity, that a player will only have one salary and one performance in 2001.
   - Order your results by player ID, least to greatest (or alphabetically by last name, as both are the same in this case!).
   - Keep in mind the lessons you’ve learned in 10.sql and 11.sql!
```sql
SELECT "first_name", "last_name" FROM (
    SELECT * FROM (
            SELECT * FROM "players"
            JOIN "salaries" ON "players"."id" = "salaries"."player_id"
            JOIN "performances" ON "salaries"."player_id" = "performances"."player_id"
            AND "salaries"."year" = "performances"."year"
            WHERE "H" != 0 AND "salaries"."year" = 2001
            ORDER BY "salary" / "H"
            LIMIT 10
    )
    INTERSECT
    SELECT * FROM (
            SELECT * FROM "players"
            JOIN "salaries" ON "players"."id" = "salaries"."player_id"
            JOIN "performances" ON "salaries"."player_id" = "performances"."player_id"
            AND "salaries"."year" = "performances"."year"
            WHERE "RBI" != 0 AND "salaries"."year" = 2001
            ORDER BY "salary" / "RBI"
            LIMIT 10
    )
)
ORDER BY "player_id";
```

## 🎯 Plan for next step
- CS50’s Introduction to Databases with SQL
  - WEEK 2
- Review WEEK 1