# 🗃️ 2025-06-09 SQL Learning Log

## 📘 Today's Learning Content
- CS50’s Introduction to Databases with SQL 
  - WEEK O 
  Learned basic SQL syntax: ables. Databases. Database Management Systems. SQL. SQLite. SELECT. LIMIT. WHERE. Comparisons. NOT. NULL. Pattern Matching. LIKE. Compound Conditions. Range Conditions. Ordering. Aggregate Functions. ROUND. DISTINCT.

- Practiced basic queries: selecting title, rating and year from a datatable 
- Learned to use `SELECT` `LIMIT` `WHERE` `NOT` `NULL` `LIKE` `ROUND`  `ORDER BY` and `DISTINCT`

---

## 💡 Key Concepts of the Day
| Concept  | English meaning                                    |
| -------- | -------------------------------------------------- |
| SELECT   | Used to select specific columns                    |
| LIMIT    | Limits the number of rows your SQL query returns   |
| WHERE    | Filters rows based on conditions                   |
| LIKE     | Find values based on a pattern, not an exact match |
| ORDER BY | Sorts the result set                               |
| DISTINCT | Removes duplicate records                          |

---

## 💡 Class notes of the Day
- basic opration
  - control+l can clear my terminal
  - control+～ open terminal/switch ternimal and code space
  - input ls -> list all of your lists
  - input sqlite3 nameoflist.db ->

- SELECT -> what data is in our database?
  " * " to say select everything, every rows every column from this table
  SELECT "title" FROM "longlist"; -> I already know there is a column called "title" in my table, so i can select title from the table.
  double quotes " " for colume names, single qoutes ' ' for sting names.

- LIMIT 
  If we try to get back a certain number of rows, for instance 5 -> LIMIT 5

- WHERE -> allows us to get back not all rows, but only some rows where some condition is true
  " = " equal, " != " not equal, " <> " equivalent to not equal

- NOT -> SELECT "title","format" FROM "longlist" WHERE NOT "format" = 'hardcover';

- AND OR () 
  Boolean logic: NOT > AND > OR
  - eg. SELECT "title" FROM "longlist" WHERE ("year" = 2022 OR "year" = 2023) AND "FORMAT" = 'hardcover'; -> (2022 or 2023) and hardcover
      SELECT "title" FROM "longlist" WHERE "year" = 2022 OR "year" = 2023 AND "format" = 'hardcover'; -> 2022 or(2023 and hardcover)

- NULL -> IS NULL / IS NOT NULL

- LIKE % _
  - ** LIKE is case-insensetive **
  The % means “zero or more characters”  THE%: starts with THE, %THE: ends with THE, %THE%: include THE
  - eg.SELECT "title" FROM "longlist" WHERE "title" LIKE '%love%';
  The _ means “Match exactly ONE character (any character)”
  - eg.SELECT "title" FROM "longlist" WHERE "title" LIKE 'P_re'; ( _ can be used more than once if necessary)

- Range Conditions > < >= <=
  - eg. SELECT "title","year"  FROM "longlist" WHERE "year" >= 2019 AND "year" <= 2022;    2019-2022
        SELECT "title","year"  FROM "longlist" WHERE "year" BETWEEN 2019 AND 2022;

- ORDER BY
  - the default ordering of ORDER BY is by ascending (from least to greatest)
  - ORDER BY ... ASC / DESC

- Aggregate Functions: COUNT / AVG / MIN / MAX / SUM
  - eg.SELECT AVG("rating") FROM "longlist";

- ROUND
  - eg.SELECT ROUND(AVG("rating"), 2) FROM "longlist"; -> SELECT ROUND(AVG("rating"), 2) AS "averagr rating" FROM "longlist";
  - Using `AS` to Rename Aggregated Columns for Clarity

When we run a query like `ROUND(AVG("rating"), 2)` without giving the column a name, the output column header will display the function expression itself:

| ROUND(AVG("rating"), 2) |
| ----------------------- |
| 3.75                    |

To make the output more readable, we can use the `AS` keyword to give the column a clear and semantic alias:

```sql
SELECT ROUND(AVG("rating"), 2) AS "average rating"
FROM longlist;
```
the output column header will display the function expression itself:

| average rating |
| -------------- |
| 3.75           |

- DISTINCT -> It removes duplicate rows from the result.
  - eg.SELECT COUNT(DISTINCT "publisher") FROM "longlist";

## 🧪 Practice Examples

```sql
-- SELECT title, rating, years FROM users;

-- SELECT * FROM lomglist WHERE rating > 4.0;

-- SELECT DISTINCT book title FROM longlist ORDER BY rating ASC;
```

## 🎯 Plan for next step
- Review 
- CS50’s Introduction to Databases with SQL
  - WEEK 0 Problem Set 0