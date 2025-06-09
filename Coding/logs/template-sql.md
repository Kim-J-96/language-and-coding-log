# 🗃️ 2025-05-27 SQL Learning Log

## 📘 Today's Learning Content
- CS50’s Introduction to Databases with SQL 
  - WEEK O 
  Learned basic SQL syntax: SELECT, FROM, WHERE
- 实践了简单查询：查询用户表中的姓名与年龄  
  Practiced basic queries: selecting name and age from a user table
- 学会使用 `DISTINCT` 去重、`ORDER BY` 排序  
  Learned to use `DISTINCT` and `ORDER BY`

---

## 💡 Key Concepts of the Day
| Concept  | Chinese meaning   | English meaning                  |
| -------- | ----------------- | -------------------------------- |
| SELECT   | ----------------- | Used to select specific columns  |
| WHERE    | ----------------- | Filters rows based on conditions |
| ORDER BY | ----------------- | Sorts the result set             |
| DISTINCT | ----------------- | Removes duplicate records        |

---

## 🧪 Practice Examples

```sql
-- 查询所有用户的名字和年龄
SELECT name, age FROM users;

-- 查询年龄大于 25 岁的用户
SELECT * FROM users WHERE age > 25;

-- 查询去重后的城市列表，并按字母排序
SELECT DISTINCT city FROM users ORDER BY city ASC;
```

## 🎯 Plan for next step
- CS50’s Introduction to Databases with SQL
  - WEEK 0 Problem Set 0
- Review 