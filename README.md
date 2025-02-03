# sql-guide-tips-tricks

## 📌 Table of Contents
- [SQL Views](#1-creating-a-view)
- [Primary Keys](#3-adding-a-primary-key)
- [Foreign Keys](#4-adding-a-foreign-key-constraint)
- [Indexes](#5-creating-an-index)
- [Queries](#6-inserting-data-into-a-table)
- [Joins](#11-using-left-join-to-combine-tables)
- [Aggregate Functions](#13-aggregate-functions)


# SQL Guide: Views, Constraints, Indexes, and Queries

## Overview
This guide covers essential SQL operations, including views, primary keys, foreign keys, indexes, and common queries. It provides explanations, examples, and memory tricks to help reinforce understanding.

---

## SQL Commands and Explanations

### 1. **Creating a View**
```sql
CREATE VIEW MyMovies AS
SELECT Title, Genre, Year
FROM Movie;
```
**Explanation:**
- A `VIEW` is a virtual table that stores a query result.
- Useful for simplifying complex queries and enhancing security by limiting data access.

**Memory Trick:** Think of a view as a saved query that behaves like a table.

---

### 2. **Dropping a View**
```sql
DROP VIEW MovieView;
```
**Explanation:**
- Removes a view from the database.
- Does NOT affect the underlying data in the original table.

---

### 3. **Adding a Primary Key**
```sql
ALTER TABLE Movie
ADD PRIMARY KEY (ID);
```
**Explanation:**
- A `PRIMARY KEY` uniquely identifies each record in a table.
- A table can have only one primary key, which must contain unique values and cannot be NULL.

**Tip:** Every table should have a primary key for data integrity.

---

### 4. **Adding a Foreign Key Constraint**
```sql
ALTER TABLE Movie
ADD CONSTRAINT Year FOREIGN KEY (Year) REFERENCES YearStats (Year);
```
**Explanation:**
- A `FOREIGN KEY` ensures referential integrity by linking records in different tables.
- This prevents invalid data entries.

**Memory Trick:** Think of a foreign key as a rule that ensures a valid relationship between tables.

---

### 5. **Creating an Index**
```sql
CREATE INDEX idx_year
ON Movie (Year);
```
**Explanation:**
- Indexes improve query performance by speeding up searches.
- `idx_year` helps queries filter or sort by `Year` faster.

**Tip:** Indexes speed up reads but slow down inserts/updates. Use them wisely!

---

### 6. **Inserting Data into a Table**
```sql
INSERT INTO Movie (Title, Genre, RatingCode, Year)
VALUES ('Pride and Prejudice', 'Romance', 'G', '2005');
```
**Explanation:**
- Adds a new record into the `Movie` table.
- Ensure the values match the column data types.

---

### 7. **Selecting All Data from a Table**
```sql
SELECT *
FROM Movie;
```
**Explanation:**
- Retrieves all records from the `Movie` table.
- The `*` wildcard selects all columns.

---

### 8. **Filtering Data with WHERE**
```sql
SELECT Title, Genre 
FROM Movie
WHERE Year = 2020;
```
**Explanation:**
- Retrieves movies released in 2020.
- The `WHERE` clause filters results.

**Memory Trick:** `WHERE` is like a filter for getting specific results.

---

### 9. **Sorting Data with ORDER BY**
```sql
SELECT Title
FROM Movie
ORDER BY Title ASC;
```
**Explanation:**
- Sorts movie titles in ascending (`ASC`) order.
- Use `DESC` for descending order.

**Tip:** `ORDER BY` ensures results appear in a specific sequence.

---

### 10. **Grouping Data with COUNT()**
```sql
SELECT RatingCode, COUNT(*) AS RatingCodeCount
FROM Movie
GROUP BY RatingCode
ORDER BY RatingCode ASC;
```
**Explanation:**
- Counts the number of movies for each rating category.
- `GROUP BY` groups rows that have the same `RatingCode`.

**Memory Trick:** `GROUP BY` is like sorting items into labeled bins before counting them.

---

### 11. **Using LEFT JOIN to Combine Tables**
```sql
SELECT Title, TotalGross
FROM Movie
LEFT JOIN YearStats ON Movie.Year = YearStats.Year;
```
**Explanation:**
- `LEFT JOIN` returns all movies and their total gross from `YearStats`.
- If no match exists in `YearStats`, NULL is returned.

**Tip:** `LEFT JOIN` keeps all rows from the left table (Movie) even if no match is found in `YearStats`.

---

### 12. **Dropping a Table**
```sql
DROP TABLE table_name;
```
**Explanation:**
- Completely removes a table and its data.
- **Use with caution!** This action cannot be undone.

**Memory Trick:** `DROP TABLE` is like permanently deleting a folder with all its files.

---

### 13. **Aggregate Functions**
- `MAX()` finds the maximum value in a set.
- `SUM()` adds up all values in a set.
- `COUNT()` counts the number of rows in a set.

**Tip:** Aggregate functions help summarize large datasets quickly.

---

### 14. **INNER JOIN**
```sql
-- INNER JOIN selects only matching left and right table rows.
```
**Explanation:**
- `INNER JOIN` returns only matching rows between two tables.
- Non-matching rows are excluded.

**Memory Trick:** `INNER JOIN` is like a strict club – only mutual members are allowed in.

---

### 15. **General Syntax for Creating Views**
```sql
CREATE VIEW ViewName [ ( Column1, Column2, ... ) ]
AS SelectStatement;
```
**Explanation:**
- Defines a view with selected columns.
- Helps simplify complex queries and enforce data security.

---

## Final Tips
- Always **backup data** before making major changes (`DROP`, `ALTER` commands).
- `INDEX` speeds up queries but adds overhead to inserts/updates.
- Use `PRIMARY KEY` and `FOREIGN KEY` constraints to maintain data integrity.
- `VIEW` simplifies queries but does not store data itself.
- `GROUP BY` is useful when working with aggregate functions like `COUNT()`.
- `ORDER BY` controls sorting order.

---

## Conclusion
This guide provides a structured explanation of fundamental SQL operations. Use the memory tricks and tips to reinforce understanding and improve database querying skills. 🚀
