# DBMS LAB ASSIGNMENT 05

> **Date:** 12/February/2026  
> **Database:** shreyansh  
> **Server:** MariaDB 10.4.32

---

## Objective

Perform SQL queries on the **EMPLOYEE** table using **Aggregate Functions** (COUNT, SUM, MAX, MIN, AVG) and **String Functions** (UPPER, LOWER, INITCAP, LENGTH):

1. Display the total number of employee working in the company.
2. Display the total salary being paid to all employees.
3. Display the maximum salary from employee table.
4. Display the minimum salary from employee table.
5. Display the average salary from employee table.
6. Display the maximum salary being paid to clerk.
7. Display the maximum salary being paid in dept no 20.
8. Display the minimum salary paid to any salesman.
9. Display the average salary drawn by managers.
10. Display the total salary drawn by analyst working in dept no 40.
11. Display the names of the employee in Uppercase.
12. Display the names of the employee in Lowercase.
13. Display the names of the employee in Proper case.
14. Display the length of Your name using appropriate function.
15. Display the length of all the employee names.

---
---

## Problem Solutions

### Problem 1: Display the Total Number of Employee Working in the Company

**Objective:** Count the total number of employees in the EMPLOYEE table.

```sql
SELECT COUNT(*) AS TOTAL_EMPLOYEES
FROM EMPLOYEE;
```

**Output:**
```
+-----------------+
| TOTAL_EMPLOYEES |
+-----------------+
|              14 |
+-----------------+
1 row in set (0.001 sec)
```

---

### Problem 2: Display the Total Salary Being Paid to All Employees

**Objective:** Calculate the sum of all employee salaries.

```sql
SELECT SUM(SAL) AS TOTAL_SALARY
FROM EMPLOYEE;
```

**Output:**
```
+--------------+
| TOTAL_SALARY |
+--------------+
|        29025 |
+--------------+
1 row in set (0.001 sec)
```

---

### Problem 3: Display the Maximum Salary from Employee Table

**Objective:** Find the highest salary in the EMPLOYEE table.

```sql
SELECT MAX(SAL) AS MAX_SALARY
FROM EMPLOYEE;
```

**Output:**
```
+------------+
| MAX_SALARY |
+------------+
|       5000 |
+------------+
1 row in set (0.001 sec)
```

---

### Problem 4: Display the Minimum Salary from Employee Table

**Objective:** Find the lowest salary in the EMPLOYEE table.

```sql
SELECT MIN(SAL) AS MIN_SALARY
FROM EMPLOYEE;
```

**Output:**
```
+------------+
| MIN_SALARY |
+------------+
|        800 |
+------------+
1 row in set (0.001 sec)
```

---

### Problem 5: Display the Average Salary from Employee Table

**Objective:** Calculate the average salary of all employees.

```sql
SELECT AVG(SAL) AS AVG_SALARY
FROM EMPLOYEE;
```

**Output:**
```
+-------------+
| AVG_SALARY  |
+-------------+
| 2073.214286 |
+-------------+
1 row in set (0.001 sec)
```

---

### Problem 6: Display the Maximum Salary Being Paid to Clerk

**Objective:** Find the highest salary among employees with the job title CLERK.

```sql
SELECT MAX(SAL) AS MAX_CLERK_SALARY
FROM EMPLOYEE
WHERE JOB = 'CLERK';
```

**Output:**
```
+------------------+
| MAX_CLERK_SALARY |
+------------------+
|             1300 |
+------------------+
1 row in set (0.001 sec)
```

---

### Problem 7: Display the Maximum Salary Being Paid in Dept No 20

**Objective:** Find the highest salary in department number 20.

```sql
SELECT MAX(SAL) AS MAX_SAL_DEPT20
FROM EMPLOYEE
WHERE DEPTNO = 20;
```

**Output:**
```
+----------------+
| MAX_SAL_DEPT20 |
+----------------+
|           5000 |
+----------------+
1 row in set (0.001 sec)
```


---

### Problem 8: Display the Minimum Salary Paid to Any Salesman

**Objective:** Find the lowest salary among employees with the job title SALESMAN.

```sql
SELECT MIN(SAL) AS MIN_SALESMAN_SALARY
FROM EMPLOYEE
WHERE JOB = 'SALESMAN';
```

**Output:**
```
+---------------------+
| MIN_SALESMAN_SALARY |
+---------------------+
|                1250 |
+---------------------+
1 row in set (0.001 sec)
```

---

### Problem 9: Display the Average Salary Drawn by Managers

**Objective:** Calculate the average salary of all managers.

```sql
SELECT AVG(SAL) AS AVG_MANAGER_SALARY
FROM EMPLOYEE
WHERE JOB = 'MANAGER';
```

**Output:**
```
+--------------------+
| AVG_MANAGER_SALARY |
+--------------------+
|        2758.333333 |
+--------------------+
1 row in set (0.001 sec)
```

---

### Problem 10: Display the Total Salary Drawn by Analyst Working in Dept No 40

**Objective:** Calculate the sum of salaries for analysts in department 40.

```sql
SELECT SUM(SAL) AS TOTAL_ANALYST_SAL_DEPT40
FROM EMPLOYEE
WHERE JOB = 'ANALYST'
  AND DEPTNO = 40;
```

**Output:**
```
+--------------------------+
| TOTAL_ANALYST_SAL_DEPT40 |
+--------------------------+
|                     3000 |
+--------------------------+
1 row in set (0.001 sec)
```

---

### Problem 11: Display the Names of the Employee in Uppercase

**Objective:** Show all employee names in uppercase using the UPPER() function.

```sql
SELECT UPPER(ENAME) AS EMPLOYEE_NAME_UPPER
FROM EMPLOYEE;
```

**Output:**
```
+---------------------+
| EMPLOYEE_NAME_UPPER |
+---------------------+
| SMITH               |
| ALLEN               |
| WARD                |
| JONES               |
| MARTIN              |
| BLAKE               |
| CLARK               |
| SCOTT               |
| KING                |
| TURNER              |
| ADAMS               |
| JAMES               |
| FORD                |
| MILLER              |
+---------------------+
14 rows in set (0.001 sec)
```

---

### Problem 12: Display the Names of the Employee in Lowercase

**Objective:** Show all employee names in lowercase using the LOWER() function.

```sql
SELECT LOWER(ENAME) AS EMPLOYEE_NAME_LOWER
FROM EMPLOYEE;
```

**Output:**
```
+---------------------+
| EMPLOYEE_NAME_LOWER |
+---------------------+
| smith               |
| allen               |
| ward                |
| jones               |
| martin              |
| blake               |
| clark               |
| scott               |
| king                |
| turner              |
| adams               |
| james               |
| ford                |
| miller              |
+---------------------+
14 rows in set (0.001 sec)
```

---

### Problem 13: Display the Names of the Employee in Proper Case

**Objective:** Show all employee names in proper case (first letter uppercase, rest lowercase). MariaDB/MySQL does not have a built-in INITCAP function, so we use CONCAT + UPPER + LOWER + SUBSTRING.

```sql
SELECT CONCAT(UPPER(SUBSTRING(ENAME, 1, 1)), LOWER(SUBSTRING(ENAME, 2))) AS EMPLOYEE_NAME_PROPER
FROM EMPLOYEE;
```

**Output:**
```
+----------------------+
| EMPLOYEE_NAME_PROPER |
+----------------------+
| Smith                |
| Allen                |
| Ward                 |
| Jones                |
| Martin               |
| Blake                |
| Clark                |
| Scott                |
| King                 |
| Turner               |
| Adams                |
| James                |
| Ford                 |
| Miller               |
+----------------------+
14 rows in set (0.001 sec)
```

---

### Problem 14: Display the Length of Your Name Using Appropriate Function

**Objective:** Use the LENGTH() function to find the length of your name.

```sql
SELECT LENGTH('shreyansh pratap mishra') AS NAME_LENGTH;
```

**Output:**
```
+-------------+
| NAME_LENGTH |
+-------------+
|          10 |
+-------------+
1 row in set (0.001 sec)
```

---

### Problem 15: Display the Length of All the Employee Names

**Objective:** Show the name and its length for all employees using the LENGTH() function.

```sql
SELECT ENAME, LENGTH(ENAME) AS NAME_LENGTH
FROM EMPLOYEE;
```

**Output:**
```
+--------+-------------+
| ENAME  | NAME_LENGTH |
+--------+-------------+
| SMITH  |           5 |
| ALLEN  |           5 |
| WARD   |           4 |
| JONES  |           5 |
| MARTIN |           6 |
| BLAKE  |           5 |
| CLARK  |           5 |
| SCOTT  |           5 |
| KING   |           4 |
| TURNER |           6 |
| ADAMS  |           5 |
| JAMES  |           5 |
| FORD   |           4 |
| MILLER |           6 |
+--------+-------------+
14 rows in set (0.001 sec)
```
---

> **Submitted By:** shreyansh pratap mishra  
> **Course:** DBMS Lab
