
# DBMS LAB ASSIGNMENT 07

> **Date:** 19/February/2026  
> **Database:** Shreyansh  
> **Server:** MariaDB 10.4.32

---

## 📋 Objective

Perform SQL queries on the **EMPLOYEE** table using **Date Computations**, **Aggregate Functions**, **GROUP BY**, **Matrix Queries**, and **Formatting**:

1. Compute the no. of days remaining in this year.
2. Find the highest and lowest salaries and the difference between of them.
3. List employee whose commission is greater than 25% of their salaries.
4. Make a query that displays salary in dollar format.
5. Create a matrix query to display the job, the salary for that job based on department number, and the total salary for that job for all departments, giving each column an appropriate heading.
6. Query that will display the total no of employees, and of that total the number who were hired in 1980, 1981, 1982 and 1983. Give appropriate column heading.
7. Query to get the last Sunday of Any Month.
8. Display department numbers and total number of employees working in each department.
9. Display the various jobs and total number of employees within each job group.
10. Display the depart numbers and total salary for each department.


---

## Problem Solutions

### Problem 1: Compute the Number of Days Remaining in This Year

**Objective:** Calculate the number of days left from today until the end of the current year.

```sql
SELECT CURDATE() AS TODAY,
       CONCAT(YEAR(CURDATE()), '-12-31') AS YEAR_END,
       DATEDIFF(CONCAT(YEAR(CURDATE()), '-12-31'), CURDATE()) AS DAYS_REMAINING;
```

**Output:**
```
+------------+------------+----------------+
| TODAY      | YEAR_END   | DAYS_REMAINING |
+------------+------------+----------------+
| 2026-02-12 | 2026-12-31 |            322 |
+------------+------------+----------------+
1 row in set (0.001 sec)
```

---

### Problem 2: Find the Highest and Lowest Salaries and the Difference Between Them

**Objective:** Display the maximum salary, minimum salary, and the difference between them.

```sql
SELECT MAX(SAL) AS HIGHEST_SALARY,
       MIN(SAL) AS LOWEST_SALARY,
       MAX(SAL) - MIN(SAL) AS DIFFERENCE
FROM EMPLOYEE;
```

**Output:**
```
+----------------+---------------+------------+
| HIGHEST_SALARY | LOWEST_SALARY | DIFFERENCE |
+----------------+---------------+------------+
|           5000 |           800 |       4200 |
+----------------+---------------+------------+
1 row in set (0.001 sec)
```

---

### Problem 3: List Employee Whose Commission Is Greater Than 25% of Their Salaries

**Objective:** Find employees where COMM > 25% of SAL.

```sql
SELECT ENAME, SAL, COMM,
       SAL * 0.25 AS SAL_25_PERCENT
FROM EMPLOYEE
WHERE COMM > SAL * 0.25;
```

**Output:**
```
+--------+------+------+----------------+
| ENAME  | SAL  | COMM | SAL_25_PERCENT |
+--------+------+------+----------------+
| MARTIN | 1250 | 1400 |         312.50 |
+--------+------+------+----------------+
1 row in set (0.001 sec)
```

---

### Problem 4: Make a Query That Displays Salary in Dollar Format

**Objective:** Display employee salaries formatted with a dollar sign ($) prefix.

```sql
SELECT ENAME,
       CONCAT('$', FORMAT(SAL, 2)) AS SALARY_IN_DOLLARS
FROM EMPLOYEE;
```

**Output:**
```
+--------+-------------------+
| ENAME  | SALARY_IN_DOLLARS |
+--------+-------------------+
| SMITH  | $800.00           |
| ALLEN  | $1,600.00         |
| WARD   | $1,250.00         |
| JONES  | $2,975.00         |
| MARTIN | $1,250.00         |
| BLAKE  | $2,850.00         |
| CLARK  | $2,450.00         |
| SCOTT  | $3,000.00         |
| KING   | $5,000.00         |
| TURNER | $1,500.00         |
| ADAMS  | $1,100.00         |
| JAMES  | $950.00           |
| FORD   | $3,000.00         |
| MILLER | $1,300.00         |
+--------+-------------------+
14 rows in set (0.001 sec)
```

---

### Problem 5: Matrix Query — Job, Salary by Department, and Total Salary

**Objective:** Create a cross-tabulation (matrix/pivot) showing each job, the salary for that job in each department, and the total salary across all departments.

```sql
SELECT JOB,
       SUM(CASE WHEN DEPTNO = 10 THEN SAL ELSE 0 END) AS DEPT_10,
       SUM(CASE WHEN DEPTNO = 20 THEN SAL ELSE 0 END) AS DEPT_20,
       SUM(CASE WHEN DEPTNO = 30 THEN SAL ELSE 0 END) AS DEPT_30,
       SUM(CASE WHEN DEPTNO = 40 THEN SAL ELSE 0 END) AS DEPT_40,
       SUM(SAL) AS TOTAL_SALARY
FROM EMPLOYEE
GROUP BY JOB
ORDER BY JOB;
```

**Output:**
```
+-----------+---------+---------+---------+---------+--------------+
| JOB       | DEPT_10 | DEPT_20 | DEPT_30 | DEPT_40 | TOTAL_SALARY |
+-----------+---------+---------+---------+---------+--------------+
| ANALYST   |       0 |    3000 |       0 |    3000 |         6000 |
| CLERK     |    1300 |    1900 |     950 |       0 |         4150 |
| MANAGER   |       0 |    5425 |    2850 |       0 |         8275 |
| PRESIDENT |       0 |    5000 |       0 |       0 |         5000 |
| SALESMAN  |       0 |       0 |    5600 |       0 |         5600 |
+-----------+---------+---------+---------+---------+--------------+
5 rows in set (0.001 sec)
```

---

### Problem 6: Total Employees and Yearly Hire Count (1980, 1981, 1982, 1983)

**Objective:** Display the total number of employees and how many were hired in each year (1980, 1981, 1982, 1983).

```sql
SELECT COUNT(*) AS TOTAL_EMPLOYEES,
       SUM(CASE WHEN YEAR(HIREDATE) = 1980 THEN 1 ELSE 0 END) AS HIRED_1980,
       SUM(CASE WHEN YEAR(HIREDATE) = 1981 THEN 1 ELSE 0 END) AS HIRED_1981,
       SUM(CASE WHEN YEAR(HIREDATE) = 1982 THEN 1 ELSE 0 END) AS HIRED_1982,
       SUM(CASE WHEN YEAR(HIREDATE) = 1983 THEN 1 ELSE 0 END) AS HIRED_1983
FROM EMPLOYEE;
```

**Output:**
```
+-----------------+------------+------------+------------+------------+
| TOTAL_EMPLOYEES | HIRED_1980 | HIRED_1981 | HIRED_1982 | HIRED_1983 |
+-----------------+------------+------------+------------+------------+
|              14 |          1 |         10 |          2 |          1 |
+-----------------+------------+------------+------------+------------+
1 row in set (0.001 sec)
```

---

### Problem 7: Query to Get the Last Sunday of Any Month

**Objective:** Find the last Sunday of the current month.

```sql
SELECT LAST_DAY(CURDATE()) AS LAST_DAY_OF_MONTH,
       DATE_SUB(LAST_DAY(CURDATE()),
           INTERVAL WEEKDAY(LAST_DAY(CURDATE()) + INTERVAL 1 DAY) DAY) AS LAST_SUNDAY;
```

**Alternative (simpler) approach:**

```sql
SELECT DATE_ADD(LAST_DAY(CURDATE()),
           INTERVAL -MOD(DAYOFWEEK(LAST_DAY(CURDATE())), 7) DAY) AS LAST_SUNDAY;
```
---

### Problem 8: Display Department Numbers and Total Number of Employees in Each Department

**Objective:** Group employees by department and count the total in each.

```sql
SELECT DEPTNO,
       COUNT(*) AS TOTAL_EMPLOYEES
FROM EMPLOYEE
GROUP BY DEPTNO
ORDER BY DEPTNO;
```

**Output:**
```
+--------+-----------------+
| DEPTNO | TOTAL_EMPLOYEES |
+--------+-----------------+
|     10 |               1 |
|     20 |               6 |
|     30 |               5 |
|     40 |               1 |
+--------+-----------------+
4 rows in set (0.001 sec)
```

---

### Problem 9: Display the Various Jobs and Total Number of Employees Within Each Job Group

**Objective:** Group employees by job title and count the total in each group.

```sql
SELECT JOB,
       COUNT(*) AS TOTAL_EMPLOYEES
FROM EMPLOYEE
GROUP BY JOB
ORDER BY TOTAL_EMPLOYEES DESC;
```

**Output:**
```
+-----------+-----------------+
| JOB       | TOTAL_EMPLOYEES |
+-----------+-----------------+
| SALESMAN  |               4 |
| CLERK     |               4 |
| MANAGER   |               3 |
| ANALYST   |               2 |
| PRESIDENT |               1 |
+-----------+-----------------+
5 rows in set (0.001 sec)
```

---

### Problem 10: Display the Department Numbers and Total Salary for Each Department

**Objective:** Show the sum of salaries grouped by department number.

```sql
SELECT DEPTNO,
       SUM(SAL) AS TOTAL_SALARY
FROM EMPLOYEE
GROUP BY DEPTNO
ORDER BY DEPTNO;
```

**Output:**
```
+--------+--------------+
| DEPTNO | TOTAL_SALARY |
+--------+--------------+
|     10 |         1300 |
|     20 |        14325 |
|     30 |        10450 |
|     40 |         3000 |
+--------+--------------+
4 rows in set (0.001 sec)
```
---

> **Submitted By:** Shreyansh pratap mishra  
> **Course:** DBMS Lab
