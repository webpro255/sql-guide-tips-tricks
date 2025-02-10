# SQL Guide: Views, Constraints, Indexes, and Queries

## 📌 Table of Contents
- [SQL Views](#1-creating-a-view)
- [Dropping a View](#2-dropping-a-view)
- [Primary Keys](#3-adding-a-primary-key)
- [Foreign Keys](#4-adding-a-foreign-key-constraint)
- [Indexes](#5-creating-an-index)
- [Inserting Data](#6-inserting-data-into-a-table)
- [Retrieving Data](#7-selecting-all-data-from-a-table)
- [Filtering Data](#8-filtering-data-with-where)
- [Sorting Data](#9-sorting-data-with-order-by)
- [Grouping Data](#10-grouping-data-with-count)
- [Joins](#11-using-left-join-to-combine-tables)
- [Dropping a Table](#12-dropping-a-table)
- [Aggregate Functions](#13-aggregate-functions)
- [INNER JOIN](#14-inner-join)
- [General Syntax for Creating Views](#15-general-syntax-for-creating-views)
- [Final Tips](#16-final-tips)

---

## **1. Creating a View**
```sql
CREATE VIEW MyMovies AS
SELECT Title, Genre, Year
FROM Movie;
```
### **Explanation:**
- A `VIEW` is a virtual table that stores a query result.
- Useful for simplifying complex queries and enhancing security by limiting data access.

### **Memory Trick:**  
Think of a view as a saved query that behaves like a table but doesn't store data.

### **Common Test Question:**
> What happens if the base table of a view is modified?  
**Answer:** The view reflects the change because it retrieves data dynamically.

---

## **2. Dropping a View**
```sql
DROP VIEW MovieView;
```
### **Explanation:**
- Removes a view from the database.
- **Does NOT affect the underlying data in the original table.**

### **Tip:**  
Use `DROP VIEW IF EXISTS MovieView;` to avoid errors if the view doesn't exist.

---

## **3. Adding a Primary Key**
```sql
ALTER TABLE Movie
ADD PRIMARY KEY (ID);
```
### **Explanation:**
- A `PRIMARY KEY` uniquely identifies each record in a table.
- A table can have **only one** primary key.
- Primary keys **must** contain unique values and cannot be `NULL`.

### **Memory Trick:**  
Think of a primary key as the **unique ID** every row must have, just like a fingerprint.

### **Common Test Question:**
> Can a table have multiple primary keys?  
**Answer:** No, but a primary key can consist of multiple columns (composite key).

---

## **4. Adding a Foreign Key Constraint**
```sql
ALTER TABLE Movie
ADD CONSTRAINT fk_year FOREIGN KEY (Year) REFERENCES YearStats (Year);
```
### **Explanation:**
- A `FOREIGN KEY` links records between tables and enforces **referential integrity**.
- Prevents inserting data that does not exist in the referenced table.

### **Memory Trick:**  
Think of a foreign key as a safety checkpoint that ensures the referenced data exists.

### **Common Test Question:**
> What happens if you try to delete a referenced row in the parent table?  
**Answer:** It depends on `ON DELETE` behavior (`CASCADE`, `SET NULL`, `NO ACTION`, etc.).

---

## **5. Creating an Index**
```sql
CREATE INDEX idx_year ON Movie (Year);
```
### **Explanation:**
- Indexes **speed up queries** by making searches faster.
- However, they slow down inserts, updates, and deletes.

### **Memory Trick:**  
Indexes are like **bookmarks** in a book—they help you find pages quickly.

### **Common Test Question:**
> Do indexes consume additional storage?  
**Answer:** Yes, because they store a sorted reference of the indexed column(s).

---

## **6. Inserting Data into a Table**
```sql
INSERT INTO Movie (Title, Genre, RatingCode, Year)
VALUES ('Pride and Prejudice', 'Romance', 'G', 2005);
```
### **Explanation:**
- Adds a new record to the `Movie` table.
- Ensure the values match the column data types.

### **Common Test Question:**
> What happens if you omit a NOT NULL column in an `INSERT` statement?  
**Answer:** The query fails unless a default value is set.

---

## **7. Selecting All Data from a Table**
```sql
SELECT * FROM Movie;
```
### **Explanation:**
- Retrieves all records from the `Movie` table.

### **Memory Trick:**  
The `*` wildcard means **"all columns"**.

---

## **8. Filtering Data with WHERE**
```sql
SELECT Title, Genre 
FROM Movie
WHERE Year = 2020;
```
### **Explanation:**
- Retrieves movies released in **2020**.
- The `WHERE` clause filters results.

### **Common Test Question:**
> What is the difference between `WHERE` and `HAVING`?  
**Answer:** `WHERE` filters individual rows, while `HAVING` filters groups.

---

## **9. Sorting Data with ORDER BY**
```sql
SELECT Title FROM Movie ORDER BY Title ASC;
```
### **Explanation:**
- Sorts movie titles **alphabetically** (`ASC` means ascending order).
- Use `DESC` for descending order.

---

## **10. Grouping Data with COUNT()**
```sql
SELECT RatingCode, COUNT(*) AS RatingCodeCount
FROM Movie
GROUP BY RatingCode;
```
### **Explanation:**
- Counts how many movies exist for each rating.

### **Memory Trick:**  
Think of `GROUP BY` as sorting items into labeled bins before counting.

---

## **11. Using LEFT JOIN to Combine Tables**
```sql
SELECT Title, TotalGross
FROM Movie
LEFT JOIN YearStats ON Movie.Year = YearStats.Year;
```
### **Explanation:**
- `LEFT JOIN` includes all rows from `Movie`, even if no match exists in `YearStats`.

---

## **12. Dropping a Table**
```sql
DROP TABLE Movie;
```
### **Explanation:**
- **Deletes the table and all its data.**
- **Use with caution!**

### **Common Test Question:**
> What is the difference between `DELETE` and `DROP`?  
**Answer:** `DELETE` removes rows but keeps the table. `DROP` removes the table entirely.

---

## **13. Aggregate Functions**
| Function | Purpose |
|----------|---------|
| `MAX()` | Finds the highest value. |
| `MIN()` | Finds the lowest value. |
| `SUM()` | Adds all values. |
| `AVG()` | Computes the average. |
| `COUNT()` | Counts rows. |

### **Common Test Question:**
> What does `COUNT(*)` do?  
**Answer:** Counts all rows, including those with NULL values.

---

## **14. INNER JOIN**
```sql
SELECT Movie.Title, YearStats.TotalGross
FROM Movie
INNER JOIN YearStats ON Movie.Year = YearStats.Year;
```
### **Explanation:**
- Returns **only matching rows** between `Movie` and `YearStats`.

### **Memory Trick:**  
An `INNER JOIN` is like a strict club—**only members with a match get in**.

---

## **15. General Syntax for Creating Views**
```sql
CREATE VIEW ViewName AS 
SELECT Column1, Column2 
FROM TableName;
```
### **Explanation:**
- Defines a view with selected columns.

---

## **16. Final Tips**
✔ **Always backup data** before using `DROP` or `ALTER TABLE`.  
✔ **Use `INDEX` for faster queries**, but don’t overuse them.  
✔ **`GROUP BY` is essential for aggregate functions** like `COUNT()`.  
✔ **Practice `JOIN` statements**—they’re crucial in real-world applications.  
✔ **`ORDER BY` is your tool for sorting data** efficiently.  

---

This version includes more **test-related questions**, **memory tricks**, and **explanations** to help you prepare and retain SQL concepts. Let me know if you'd like more additions! 🚀
