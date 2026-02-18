
# DBMS LAB ASSIGNMENT 03

> **Date:** 04/February/2026  
> **Database:** SHREYANSH 
> **Server:** MariaDB 10.4.32

---

## Objective

Perform advanced data retrieval queries using **ORDER BY**, **LIKE patterns**, **IN**, **IS NULL**, and **calculated columns**:

1. List all employees and jobs in Department 30 in descending order of salary
2. List job and department number of employees whose name is five letters long, starts with 'A' and ends with 'N'
3. Display the names of employees whose name starts with 'S'
4. Display the names of employees whose name ends with 'S'
5. Display names of employees working in department 10, 20, or 40 OR working as clerk, salesman, or analyst
6. Display employee number and names for employees who earn commission
7. Display employee number and total salary for each employee
8. Display employee number and annual salary for each employee
9. Display names of all employees working as clerks and earning more than 3000
10. Display names of employees working as clerk, salesman, or analyst and earning more than 3000

---

## Problem Solutions

### Problem 1: List All Employees and Jobs in Department 30 (Descending Order of Salary)

**Objective:** Retrieve employees from Department 30 sorted by salary in descending order.

```sql
SELECT ENAME, JOB, SAL
FROM EMPLOYEE
WHERE DEPTNO = 30
ORDER BY SAL DESC;
```

**Output:**
```
+--------+----------+------+
| ENAME  | JOB      | SAL  |
+--------+----------+------+
| BLAKE  | MANAGER  | 2850 |
| ALLEN  | SALESMAN | 1600 |
| TURNER | SALESMAN | 1500 |
| WARD   | SALESMAN | 1250 |
| MARTIN | SALESMAN | 1250 |
| JAMES  | CLERK    |  950 |
+--------+----------+------+
6 rows in set (0.001 sec)
```


---

### Problem 2: Employees Whose Name is 5 Letters, Starts with 'A' and Ends with 'N'

**Objective:** Use pattern matching to find employees with specific name format.

```sql
SELECT JOB, DEPTNO
FROM EMPLOYEE
WHERE ENAME LIKE 'A___N';
```

> **Note:** Each underscore `_` represents exactly one character.

**Output:**
```
+----------+--------+
| JOB      | DEPTNO |
+----------+--------+
| SALESMAN |     30 |
+----------+--------+
1 row in set (0.001 sec)
```

---

### Problem 3: Display Names of Employees Whose Name Starts with 'S'

**Objective:** Find employees whose name begins with the letter 'S'.

```sql
SELECT ENAME
FROM EMPLOYEE
WHERE ENAME LIKE 'S%';
```

**Output:**
```
+-------+
| ENAME |
+-------+
| SMITH |
| SCOTT |
+-------+
2 rows in set (0.001 sec)
```


---

### Problem 4: Display Names of Employees Whose Name Ends with 'S'

**Objective:** Find employees whose name ends with the letter 'S'.

```sql
SELECT ENAME
FROM EMPLOYEE
WHERE ENAME LIKE '%S';
```

**Output:**
```
+-------+
| ENAME |
+-------+
| JONES |
| ADAMS |
| JAMES |
+-------+
3 rows in set (0.001 sec)
```


---

### Problem 5: Employees in Department 10/20/40 OR Working as Clerk/Salesman/Analyst

**Objective:** Use compound conditions with `OR` and `IN` operators.

```sql
SELECT ENAME
FROM EMPLOYEE
WHERE DEPTNO IN (10, 20, 40)
OR JOB IN ('CLERK', 'SALESMAN', 'ANALYST');
```

**Output:**
```
+--------+
| ENAME  |
+--------+
| SMITH  |
| ALLEN  |
| WARD   |
| JONES  |
| MARTIN |
| CLARK  |
| SCOTT  |
| KING   |
| TURNER |
| ADAMS  |
| JAMES  |
| FORD   |
| MILLER |
+--------+
13 rows in set (0.001 sec)
```


---

### Problem 6: Employees Who Earn Commission

**Objective:** Find employees with non-null and positive commission values.

```sql
SELECT EMPNO, ENAME
FROM EMPLOYEE
WHERE COMM IS NOT NULL
AND COMM > 0;
```

**Output:**
```
+-------+--------+
| EMPNO | ENAME  |
+-------+--------+
|  7499 | ALLEN  |
|  7521 | WARD   |
|  7654 | MARTIN |
+-------+--------+
3 rows in set (0.001 sec)
```


---

### Problem 7: Display Employee Number and Total Salary (Salary + Commission)

**Objective:** Calculate total salary including commission using `IFNULL()` function.

```sql
SELECT EMPNO, (SAL + IFNULL(COMM, 0)) AS TOTAL_SALARY
FROM EMPLOYEE;
```

>  **Note:** `IFNULL(COMM, 0)` returns 0 if COMM is NULL (MySQL/MariaDB).  


**Output:**
```
+-------+--------------+
| EMPNO | TOTAL_SALARY |
+-------+--------------+
|  7369 |          800 |
|  7499 |         1900 |
|  7521 |         1550 |
|  7566 |         2975 |
|  7654 |         2650 |
|  7698 |         2850 |
|  7782 |         2450 |
|  7788 |         3000 |
|  7839 |         5000 |
|  7844 |         1500 |
|  7876 |         1100 |
|  7900 |          950 |
|  7902 |         3000 |
|  7934 |         1300 |
+-------+--------------+
14 rows in set (0.001 sec)
```

> **Result:** Total salary calculated for all 14 employees

---

### Problem 8: Display Employee Number and Annual Salary

**Objective:** Calculate annual salary (monthly salary × 12).

```sql
SELECT EMPNO, (SAL * 12) AS ANNUAL_SALARY
FROM EMPLOYEE;
```

**Output:**
```
+-------+---------------+
| EMPNO | ANNUAL_SALARY |
+-------+---------------+
|  7369 |          9600 |
|  7499 |         19200 |
|  7521 |         15000 |
|  7566 |         35700 |
|  7654 |         15000 |
|  7698 |         34200 |
|  7782 |         29400 |
|  7788 |         36000 |
|  7839 |         60000 |
|  7844 |         18000 |
|  7876 |         13200 |
|  7900 |         11400 |
|  7902 |         36000 |
|  7934 |         15600 |
+-------+---------------+
14 rows in set (0.001 sec)
```

---

### Problem 9: Clerks Earning More Than 3000

**Objective:** Find clerks with salary greater than 3000.

```sql
SELECT ENAME
FROM EMPLOYEE
WHERE JOB = 'CLERK'
AND SAL > 3000;
```

**Output:**
```
Empty set (0.001 sec)
```

---

### Problem 10: Clerks, Salesmen, or Analysts Earning More Than 3000

**Objective:** Find employees in specific jobs earning more than 3000.

```sql
SELECT ENAME
FROM EMPLOYEE
WHERE JOB IN ('CLERK', 'SALESMAN', 'ANALYST')
AND SAL > 3000;
```

**Output:**
```
Empty set (0.001 sec)
```
---

---

> **Submitted By:** SHREYANSH PRATAP MISHRA
> **Course:** DBMS Lab
> **OS:** MacOS used
