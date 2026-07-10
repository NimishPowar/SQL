

# 📘 SQL Handbook 



# 1. Basic Query Structure

### Syntax

```sql
SELECT column_name
FROM table_name;
```

Example:

```sql
SELECT name
FROM Employee;
```

---

# 2. WHERE Clause

Filters rows based on conditions.

```sql
SELECT *
FROM Employee
WHERE salary > 50000;
```

Operators:

```sql
=
!=
>
<
>=
<=
```

Logical operators:

```sql
AND
OR
NOT
```

---

# 3. NULL Handling

❌ Wrong

```sql
WHERE referee_id = NULL
```

```sql
WHERE referee_id != NULL
```

✅ Correct

```sql
WHERE referee_id IS NULL
```

```sql
WHERE referee_id IS NOT NULL
```

**Remember:**

`NULL` is **not a value**.

It means **missing/unknown**.

---

# 4. DISTINCT

Removes duplicate rows.

```sql
SELECT DISTINCT author_id
FROM Views;
```

---

# 5. Column Alias (`AS`)

Rename columns in the output.

```sql
SELECT AVG(salary) AS average_salary
FROM Employee;
```

---

# 6. ORDER BY

Sort results.

Ascending (default)

```sql
ORDER BY salary;
```

Descending

```sql
ORDER BY salary DESC;
```

---

# 7. String Function

Length of string

```sql
LENGTH(column_name)
```

Example

```sql
SELECT tweet_id
FROM Tweets
WHERE LENGTH(content) > 15;
```

---

# 8. Aggregate Functions

## COUNT

Counts rows.

```sql
COUNT(*)
```

Counts all rows.

```sql
COUNT(column)
```

Counts only non-null values.

---

## SUM

```sql
SUM(salary)
```

---

## AVG

```sql
AVG(salary)
```

---

## MAX

```sql
MAX(salary)
```

---

## MIN

```sql
MIN(salary)
```

---

# 9. GROUP BY ⭐⭐⭐

Groups rows before applying aggregate functions.

Example:

```sql
SELECT Department,
       COUNT(*)
FROM Employee
GROUP BY Department;
```

Pattern:

```sql
SELECT group_column,
       AGGREGATE_FUNCTION(column)
FROM table
GROUP BY group_column;
```

Examples:

```sql
COUNT()
SUM()
AVG()
MAX()
MIN()
```

---

# 10. HAVING ⭐⭐⭐

Filters groups.

Execution order:

```
Rows
↓

WHERE
↓

GROUP BY
↓

Aggregate Functions
↓

HAVING
↓

Result
```

Example:

```sql
SELECT Department,
       AVG(Salary)
FROM Employee
GROUP BY Department
HAVING AVG(Salary) > 45000;
```

---

# 11. JOIN

Combines data from multiple tables.

General syntax:

```sql
SELECT columns
FROM table1
JOIN table2
ON table1.id = table2.id;
```

---

# 12. INNER JOIN

Returns only matching rows.

```sql
SELECT *
FROM Employee e
JOIN Salary s
ON e.id = s.id;
```

Think:

> **Only matching records.**

---

# 13. LEFT JOIN ⭐⭐⭐

Keeps all rows from the left table.

```sql
SELECT *
FROM Employee e
LEFT JOIN Salary s
ON e.id = s.id;
```

Think:

> **Keep everything on the left.**

Useful when the question says:

* Include everyone
* Even if no record exists
* Show customers without orders
* Show employees without salaries

---

# 14. SELF JOIN ⭐⭐⭐

Compare rows from the same table.

Syntax:

```sql
SELECT *
FROM Employee e1
JOIN Employee e2
ON e1.manager_id = e2.id;
```

Important:

There is **no**

```sql
SELF JOIN
```

keyword.

---

# 15. SQL Execution Order ⭐⭐⭐⭐⭐

Always remember this:

```
FROM

↓

JOIN

↓

ON

↓

WHERE

↓

GROUP BY

↓

HAVING

↓

SELECT

↓

ORDER BY
```

This explains why:

❌

```sql
WHERE COUNT(*) > 2
```

doesn't work.

Because `COUNT()` doesn't exist until after `GROUP BY`.

---

# 16. SQL Interview Patterns

### Pattern 1

Filter rows

```sql
SELECT ...
FROM ...
WHERE ...
```

---

### Pattern 2

Find missing records

```sql
LEFT JOIN

WHERE right_table.column IS NULL
```

---

### Pattern 3

Count per category

```sql
GROUP BY category
COUNT(*)
```

---

### Pattern 4

Average per category

```sql
GROUP BY category
AVG(column)
```

---

### Pattern 5

Filter groups

```sql
GROUP BY ...

HAVING ...
```

---

### Pattern 6

Compare rows in the same table

```sql
SELF JOIN
```

(using `JOIN` with aliases)

---
