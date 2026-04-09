# 🗄️ SQL & DBMS Challenges

---

## 🟢 01 — Find Duplicate Emails

### Problem
Write a SQL query to find all duplicate emails in a table called `Person`.

```
Person table:
+----+---------+
| Id | Email   |
+----+---------+
| 1  | a@b.com |
| 2  | c@d.com |
| 3  | a@b.com |
+----+---------+
```

**Output:** `a@b.com`

### Solution
```sql
SELECT Email
FROM Person
GROUP BY Email
HAVING COUNT(Email) > 1;
```

---

## 🟡 02 — Second Highest Salary

### Problem
Write a SQL query to get the **second highest** salary from the `Employee` table. Return `NULL` if it doesn't exist.

### Solution
```sql
SELECT MAX(Salary) AS SecondHighestSalary
FROM Employee
WHERE Salary < (SELECT MAX(Salary) FROM Employee);
```

#### Alternative using LIMIT/OFFSET:
```sql
SELECT IFNULL(
    (SELECT DISTINCT Salary FROM Employee
     ORDER BY Salary DESC
     LIMIT 1 OFFSET 1),
    NULL
) AS SecondHighestSalary;
```

---

## 🟢 03 — Employees Earning More Than Managers

### Problem
Write a SQL query to find employees who earn more than their managers.

```
Employee table:
+----+-------+--------+-----------+
| Id | Name  | Salary | ManagerId |
+----+-------+--------+-----------+
| 1  | Joe   | 70000  | 3         |
| 2  | Henry | 80000  | 4         |
| 3  | Sam   | 60000  | NULL      |
| 4  | Max   | 90000  | NULL      |
+----+-------+--------+-----------+
```

**Output:** `Joe`

### Solution
```sql
SELECT e1.Name AS Employee
FROM Employee e1
JOIN Employee e2 ON e1.ManagerId = e2.Id
WHERE e1.Salary > e2.Salary;
```

---

## 🟡 04 — Rank Scores

### Problem
Write a SQL query to rank scores. If two scores are tied, they should have the same rank. Ranks should not have gaps.

### Solution
```sql
SELECT Score,
       DENSE_RANK() OVER (ORDER BY Score DESC) AS Rank
FROM Scores
ORDER BY Score DESC;
```

---

## 🔴 05 — Department Top 3 Salaries

### Problem
Find employees who have one of the **top 3 unique salaries** in each department.

### Solution
```sql
SELECT d.Name AS Department, e.Name AS Employee, e.Salary
FROM Employee e
JOIN Department d ON e.DepartmentId = d.Id
WHERE (
    SELECT COUNT(DISTINCT e2.Salary)
    FROM Employee e2
    WHERE e2.DepartmentId = e.DepartmentId
    AND e2.Salary > e.Salary
) < 3
ORDER BY d.Name, e.Salary DESC;
```

#### Alternative using DENSE_RANK:
```sql
WITH RankedSalaries AS (
    SELECT e.Name, e.Salary, d.Name AS Department,
           DENSE_RANK() OVER (PARTITION BY e.DepartmentId ORDER BY e.Salary DESC) AS rnk
    FROM Employee e
    JOIN Department d ON e.DepartmentId = d.Id
)
SELECT Department, Name AS Employee, Salary
FROM RankedSalaries
WHERE rnk <= 3;
```

---

## 📌 DBMS Key Concepts

### Normalization
| Form | Rule |
|------|------|
| 1NF | Atomic values, no repeating groups |
| 2NF | 1NF + no partial dependencies |
| 3NF | 2NF + no transitive dependencies |
| BCNF | Every determinant is a candidate key |

### Important SQL Clauses
```sql
-- Window Functions
ROW_NUMBER(), RANK(), DENSE_RANK(), NTILE()
LEAD(), LAG(), FIRST_VALUE(), LAST_VALUE()

-- Aggregate
COUNT(), SUM(), AVG(), MIN(), MAX()

-- Joins
INNER JOIN, LEFT JOIN, RIGHT JOIN, FULL OUTER JOIN, CROSS JOIN, SELF JOIN

-- Set Operations
UNION, UNION ALL, INTERSECT, EXCEPT
```

### Indexes
```sql
CREATE INDEX idx_name ON table_name(column_name);
CREATE UNIQUE INDEX idx_name ON table_name(column_name);
```

### Transactions
```sql
BEGIN;
  UPDATE accounts SET balance = balance - 500 WHERE id = 1;
  UPDATE accounts SET balance = balance + 500 WHERE id = 2;
COMMIT;
-- or ROLLBACK; if something goes wrong
```

---

## 🔗 Practice Links
- [LeetCode SQL Problems](https://leetcode.com/problemset/database/)
- [HackerRank SQL](https://www.hackerrank.com/domains/sql)
- [SQLZoo](https://sqlzoo.net)
- [StrataScratch](https://www.stratascratch.com)

---

*Part of [NutanGarage Coding Challenges](../README.md)*
