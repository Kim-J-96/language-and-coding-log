# 🗃️ 2025-06-13 ~ 20 SQL Learning Log

## 📘 Today's Learning Content
- CS50’s Introduction to Databases with SQL 
  - WEEK 1 
    - Relational Databases. Relationships: One-to-one, One-to-many, Many-to-many. Entity Relationship Diagrams. 
     ![notation](CS50_SQL/images/ER_Diagram_notation.png)
    - Keys: Primary Keys, Foreign Keys. Subqueries(also called nested queries). IN. 
    - Joins: INNER JOIN, Outer Joins, LEFT JOIN, RIGHT JOIN, FULL JOIN, NATURAL JOIN. 
    - Sets: INTERSECT, UNION, EXCEPT. 
    - Groups: GROUP BY, HAVING.

- Learned to use `IN` `INNER JOIN,` `LEFT JOIN` `RIGHT JOIN` `FULL JOIN` `NATURAL JOIN` `INTERSECT`  `UNION` `EXCEPT` `GROUP BY` and `HAVING`

---

## 💡 Key Concepts of the Day
| Concept      | English meaning                                                     |
| ------------ | ------------------------------------------------------------------- |
| Primary Keys | an identifier that is unique for every item in a table              |
| Foreign Keys | A foreign key is a primary key taken from a different table         |
| IN           | check whether the desired value is in a given list or set of values |
| JOIN         | allows us to combine two or more tables together                    |
| NATURAL JOIN | can remove a duplicate id column                                    |
| HAVING       | used here to specify a condition for the groups                     |

---

## 💡 Class notes of the Day
-- Relational Databases. Relationships: One-to-one, One-to-many, Many-to-many. Entity Relationship Diagrams(ER Diagrams).
-- Keys: Primary Keys, Foreign Keys. Subqueries. IN.

```sql
SELECT "id" FROM "publishers"
WHERE "publisher" = 'MacLehose Press';
```

- The example for a one-to-many relationship.

```sql
SELECT "title" FROM "books"
WHERE "publisher_id" = (
    SELECT "id" FROM "publishers"
    WHERE "publisher" = 'MacLehose Press'
);
```

- The example is for many-to-many relationships. To find the author(s) who wrote the book Flights

```sql
SELECT "name" FROM "authors"
WHERE "id" = (
     SELECT "author_id" FROM "authored"
     WHERE "book_id" = (
          SELECT "id" FROM "books"
          WHERE "title" = 'Flights'
    )
);
```

- IN - This keyword is used to check whether the desired value is in a given list or set of values.

```sql
SELECT "title" from "books"
WHERE "id" IN (
     SELECT "book_id" FROM "authored"
     WHERE "author_id" = (
         SELECT "id" FROM "authors"
         WHERE "name" = 'Fernanda Melchor'
     )
 );
 ```

-- Joins: INNER JOIN, Outer Joins, LEFT JOIN, RIGHT JOIN, FULL JOIN, NATURAL JOIN.

```sql
SELECT * FROM "sea_lions"
JOIN "migrations" ON "migrations"."id" = "sea_lions"."id";
```

- LEFT JOIN, RIGHT JOIN and FULL JOIN are called OUTER JOIN.
A LEFT JOIN prioritizes the data in the left (or first) table.

```sql
SELECT * FROM "sea_lions"
LEFT JOIN "migrations" ON "migrations"."id" = "sea_lions"."id";
```

- Similarly, a RIGHT JOIN retains all the rows from the right (or second) table.
- A FULL JOIN allows us to see the entirety of all tables.

```sql
SELECT * FROM "sea_lions"
RIGHT JOIN "migrations" ON "migrations"."id" = "sea_lions"."id";
```

```sql
SELECT * FROM "sea_lions"
FULL JOIN "migrations" ON "migrations"."id" = "sea_lions"."id";
```

- NATURAL JOIN can remove a duplicate id column.

```sql
SELECT * FROM "sea_lions"
NATURAL JOIN "migrations";
```

-- Sets: INTERSECT, UNION, EXCEPT.

```sql
SELECT "name" FROM "translators"
INTERSECT
SELECT "name" FROM "authors";
```

- If a person is either an author or a translator, or both, they belong to the union of the two sets.

```sql
SELECT "name" FROM "translators"
UNION
SELECT "name" FROM "authors";
```

- ONLY translators

```sql
SELECT "name" FROM "translators"
EXCEPT
SELECT "name" FROM "authors";
```

- ONLY authors

```sql
SELECT "name" FROM "authors"
EXCEPT
SELECT "name" FROM "translators";
```

- A minor adjustment to the previous query gives us the profession of the person in the result set, based on whether they are an author or a translator.

```sql
SELECT 'author' AS "profession", "name"
FROM "authors"
UNION
SELECT 'translator' AS "profession", "name"
FROM "translators";
```

```sql
SELECT "book_id" FROM "translated"
WHERE "translator_id" = (
    SELECT "id" FROM "translators"
    WHERE "name" = 'Sophie Hughes'
)
INTERSECT
SELECT "book_id" FROM "translated"
WHERE "translator_id" = (
    SELECT "id" FROM "translators"
    WHERE "name" = 'Margaret Jull Costa'
);
```

-- Groups: GROUP BY, HAVING.

```sql
SELECT "book_id", AVG("rating") FROM "ratings"
GROUP BY "book_id";
```

```sql
SELECT "book_id", ROUND(AVG("rating"), 2) AS "average rating"
FROM "ratings"
GROUP BY "book_id"
HAVING "average rating" > 4.0;
```

## 🧪 Practice Examples

```sql
-- SELECT title, rating, years FROM users;

-- SELECT * FROM lomglist WHERE rating > 4.0;

-- SELECT DISTINCT book title FROM longlist ORDER BY rating ASC;
```

## 🎯 Plan for next step
- Review 
- CS50’s Introduction to Databases with SQL
  - WEEK 1 Problem Set 1