# DBMS LAB ASSIGNMENT 06

> **Date:** 12/February/2026  
> **Database:** shreyansh  
> **Server:** MariaDB 10.4.32

---

## Objective

Perform SQL queries on the **EMPLOYEE** table using **Date Functions**, **CASE (DECODE equivalent)**, and **String Functions**:

1. Display empno, ename, deptno from employee table. Instead of display department numbers display the related department name (Use decode function).
2. Display your age in days.
3. Display your age in months.
4. Display the current date as 15th August Friday Nineteen Ninety-Seven.
5. Display the following output for each row from employee table.
6. Scott has joined the company on Wednesday 13th August Nineteen Ninety.
7. Find the date for nearest Saturday after current date.
8. Display current time.
9. Display the date three months Before the current date.
10. Display those employees who joined in the company in the month of Dec.
11. Display those employees whose first 2 characters from hire date - last 2 characters of salary.
12. Display those employees whose 10% of salary is equal to the year of joining.
13. Display those employees who joined the company before 15 of the months.
14. Display those employees who has joined before 15th of the month.
15. Display those employees whose joining DATE is available in deptno.

---

## Problem Solutions

### Problem 1: Display Empno, Ename, Deptno with Department Name (Using CASE/DECODE)

**Objective:** Replace department numbers with their corresponding department names using CASE (MySQL/MariaDB equivalent of Oracle's DECODE function).

```sql
SELECT EMPNO, ENAME,
       CASE DEPTNO
           WHEN 10 THEN 'ACCOUNTING'
           WHEN 20 THEN 'RESEARCH'
           WHEN 30 THEN 'SALES'
           WHEN 40 THEN 'OPERATIONS'
       END AS DEPARTMENT_NAME
FROM EMPLOYEE;
```

> **Note:** Oracle uses `DECODE(DEPTNO, 10, 'ACCOUNTING', 20, 'RESEARCH', ...)` but MySQL/MariaDB uses the `CASE WHEN` statement as the equivalent.

**Output:**
```
+-------+--------+-----------------+
| EMPNO | ENAME  | DEPARTMENT_NAME |
+-------+--------+-----------------+
|  7369 | SMITH  | RESEARCH        |
|  7499 | ALLEN  | SALES           |
|  7521 | WARD   | SALES           |
|  7566 | JONES  | RESEARCH        |
|  7654 | MARTIN | SALES           |
|  7698 | BLAKE  | SALES           |
|  7782 | CLARK  | RESEARCH        |
|  7788 | SCOTT  | OPERATIONS      |
|  7839 | KING   | RESEARCH        |
|  7844 | TURNER | SALES           |
|  7876 | ADAMS  | RESEARCH        |
|  7900 | JAMES  | SALES           |
|  7902 | FORD   | RESEARCH        |
|  7934 | MILLER | ACCOUNTING      |
+-------+--------+-----------------+
14 rows in set (0.001 sec)
```

---

### Problem 2: Display Your Age in Days

**Objective:** Calculate your age in days using the DATEDIFF() function.

```sql
SELECT DATEDIFF(CURDATE(), '2005-08-15') AS AGE_IN_DAYS;
```

> **Note:** Replace `'2005-08-15'` with your actual date of birth.

**Output:**
```
+-------------+
| AGE_IN_DAYS |
+-------------+
|        7486 |
+-------------+
1 row in set (0.001 sec)
```

---

### Problem 3: Display Your Age in Months

**Objective:** Calculate your age in months using the TIMESTAMPDIFF() function.

```sql
SELECT TIMESTAMPDIFF(MONTH, '2005-08-15', CURDATE()) AS AGE_IN_MONTHS;
```

> **Note:** Replace `'2005-08-15'` with your actual date of birth.

**Output:**
```
+---------------+
| AGE_IN_MONTHS |
+---------------+
|           245 |
+---------------+
1 row in set (0.001 sec)
```

---

### Problem 4: Display the Current Date in Formatted Style

**Objective:** Display the current date in the format: **"12th February Thursday 2026"** (equivalent to Oracle's `TO_CHAR(SYSDATE, 'DDth Month Day Year')`).

```sql
SELECT DATE_FORMAT(CURDATE(), '%D %M %W %Y') AS FORMATTED_DATE;
```

**Output:**
```
+----------------------------------+
| FORMATTED_DATE                   |
+----------------------------------+
| 12th February Thursday 2026     |
+----------------------------------+
1 row in set (0.001 sec)
```
---

### Problem 5: Display Formatted Joining Details for Each Employee

**Objective:** Display a formatted sentence for each employee showing their joining details.

**Expected Format:** `ENAME has joined the company on DAYNAME Dth MONTHNAME YEAR`

```sql
SELECT CONCAT(ENAME, ' has joined the company on ',
       DAYNAME(HIREDATE), ' ',
       DATE_FORMAT(HIREDATE, '%D'), ' ',
       MONTHNAME(HIREDATE), ' ',
       YEAR(HIREDATE)) AS EMPLOYEE_JOINING
FROM EMPLOYEE;
```

**Output:**
```
+-----------------------------------------------------------------------+
| EMPLOYEE_JOINING                                                      |
+-----------------------------------------------------------------------+
| SMITH has joined the company on Wednesday 17th December 1980          |
| ALLEN has joined the company on Friday 20th February 1981             |
| WARD has joined the company on Sunday 22nd February 1981              |
| JONES has joined the company on Thursday 2nd April 1981               |
| MARTIN has joined the company on Monday 28th September 1981           |
| BLAKE has joined the company on Friday 1st May 1981                   |
| CLARK has joined the company on Tuesday 9th June 1981                 |
| SCOTT has joined the company on Thursday 9th December 1982            |
| KING has joined the company on Tuesday 17th November 1981             |
| TURNER has joined the company on Tuesday 8th September 1981           |
| ADAMS has joined the company on Wednesday 12th January 1983           |
| JAMES has joined the company on Thursday 3rd December 1981            |
| FORD has joined the company on Thursday 3rd December 1981             |
| MILLER has joined the company on Saturday 23rd January 1982           |
+-----------------------------------------------------------------------+
14 rows in set (0.001 sec)
```

---

### Problem 6: Display Specific Employee Joining Detail (SCOTT)

**Objective:** Display Scott's joining information in the formatted sentence style.

```sql
SELECT CONCAT(ENAME, ' has joined the company on ',
       DAYNAME(HIREDATE), ' ',
       DATE_FORMAT(HIREDATE, '%D'), ' ',
       MONTHNAME(HIREDATE), ' ',
       YEAR(HIREDATE)) AS EMPLOYEE_JOINING
FROM EMPLOYEE
WHERE ENAME = 'SCOTT';
```

**Output:**
```
+--------------------------------------------------------------+
| EMPLOYEE_JOINING                                             |
+--------------------------------------------------------------+
| SCOTT has joined the company on Thursday 9th December 1982   |
+--------------------------------------------------------------+
1 row in set (0.001 sec)
```

---

### Problem 7: Find the Date for Nearest Saturday After Current Date

**Objective:** Calculate the next Saturday from today's date.

```sql
SELECT CURDATE() AS TODAY,
       DATE_ADD(CURDATE(),
           INTERVAL MOD(5 - WEEKDAY(CURDATE()) + 7, 7) DAY) AS NEXT_SATURDAY;
```

**Explanation:**
- `WEEKDAY()` returns 0=Monday, 1=Tuesday, ..., 5=Saturday, 6=Sunday
- Formula `MOD(5 - WEEKDAY(CURDATE()) + 7, 7)` calculates days until next Saturday
- For Thursday (WEEKDAY=3): `MOD(5-3+7, 7)` = `MOD(9,7)` = **2 days**

**Output:**
```
+------------+---------------+
| TODAY      | NEXT_SATURDAY |
+------------+---------------+
| 2026-02-12 | 2026-02-14    |
+------------+---------------+
1 row in set (0.001 sec)
```

---

### Problem 8: Display Current Time

**Objective:** Display the current system time.

```sql
SELECT CURTIME() AS CURRENT_TIME;
```

**Output:**
```
+--------------+
| CURRENT_TIME |
+--------------+
| 00:29:00     |
+--------------+
1 row in set (0.001 sec)
```

---

### Problem 9: Display the Date Three Months Before the Current Date

**Objective:** Calculate and display the date that is 3 months before today.

```sql
SELECT CURDATE() AS TODAY,
       DATE_SUB(CURDATE(), INTERVAL 3 MONTH) AS THREE_MONTHS_BEFORE;
```

**Output:**
```
+------------+---------------------+
| TODAY      | THREE_MONTHS_BEFORE |
+------------+---------------------+
| 2026-02-12 | 2025-11-12          |
+------------+---------------------+
1 row in set (0.001 sec)
```

---

### Problem 10: Display Employees Who Joined in the Month of December

**Objective:** Retrieve employees whose hire date falls in the month of December.

```sql
SELECT ENAME, HIREDATE
FROM EMPLOYEE
WHERE MONTH(HIREDATE) = 12;
```

**Output:**
```
+-------+------------+
| ENAME | HIREDATE   |
+-------+------------+
| SMITH | 1980-12-17 |
| SCOTT | 1982-12-09 |
| JAMES | 1981-12-03 |
| FORD  | 1981-12-03 |
+-------+------------+
4 rows in set (0.001 sec)
```

---

### Problem 11: Display First 2 Characters from Hire Date and Last 2 Characters of Salary

**Objective:** Concatenate the first 2 characters of the HIREDATE with the last 2 characters of the salary for each employee.

```sql
SELECT ENAME,
       HIREDATE,
       SAL,
       CONCAT(LEFT(HIREDATE, 2), RIGHT(CAST(SAL AS CHAR), 2)) AS RESULT
FROM EMPLOYEE;
```

**Output:**
```
+--------+------------+------+--------+
| ENAME  | HIREDATE   | SAL  | RESULT |
+--------+------------+------+--------+
| SMITH  | 1980-12-17 |  800 | 1900   |
| ALLEN  | 1981-02-20 | 1600 | 1900   |
| WARD   | 1981-02-22 | 1250 | 1950   |
| JONES  | 1981-04-02 | 2975 | 1975   |
| MARTIN | 1981-09-28 | 1250 | 1950   |
| BLAKE  | 1981-05-01 | 2850 | 1950   |
| CLARK  | 1981-06-09 | 2450 | 1950   |
| SCOTT  | 1982-12-09 | 3000 | 1900   |
| KING   | 1981-11-17 | 5000 | 1900   |
| TURNER | 1981-09-08 | 1500 | 1900   |
| ADAMS  | 1983-01-12 | 1100 | 1900   |
| JAMES  | 1981-12-03 |  950 | 1950   |
| FORD   | 1981-12-03 | 3000 | 1900   |
| MILLER | 1982-01-23 | 1300 | 1900   |
+--------+------------+------+--------+
14 rows in set (0.001 sec)
```

---

### Problem 12: Display Employees Whose 10% of Salary Equals the Year of Joining

**Objective:** Find employees where 10% of their salary equals the last two digits of their joining year.

```sql
SELECT ENAME, SAL,
       SAL * 0.10 AS TEN_PERCENT,
       YEAR(HIREDATE) % 100 AS YEAR_LAST2
FROM EMPLOYEE
WHERE SAL * 0.10 = YEAR(HIREDATE) % 100;
```

**Explanation:** Since full YEAR values (1980-1983) are much larger than 10% of any salary, the comparison uses the last 2 digits of the year.

**Output:**
```
+-------+-----+-------------+------------+
| ENAME | SAL | TEN_PERCENT | YEAR_LAST2 |
+-------+-----+-------------+------------+
| SMITH | 800 |       80.00 |         80 |
+-------+-----+-------------+------------+
1 row in set (0.001 sec)
```

---

### Problem 13: Display Employees Who Joined Before 15th of the Month

**Objective:** Retrieve employees whose hire day-of-month is less than 15.

```sql
SELECT ENAME, HIREDATE, DAY(HIREDATE) AS JOIN_DAY
FROM EMPLOYEE
WHERE DAY(HIREDATE) < 15;
```

**Output:**
```
+--------+------------+----------+
| ENAME  | HIREDATE   | JOIN_DAY |
+--------+------------+----------+
| JONES  | 1981-04-02 |        2 |
| BLAKE  | 1981-05-01 |        1 |
| CLARK  | 1981-06-09 |        9 |
| SCOTT  | 1982-12-09 |        9 |
| TURNER | 1981-09-08 |        8 |
| ADAMS  | 1983-01-12 |       12 |
| JAMES  | 1981-12-03 |        3 |
| FORD   | 1981-12-03 |        3 |
+--------+------------+----------+
8 rows in set (0.001 sec)
```

---

### Problem 14: Display Employees Who Joined Before 15th of the Month

**Objective:** Retrieve employees who joined on a day earlier than the 15th of the month (alternative approach using DATE_FORMAT).

```sql
SELECT ENAME, HIREDATE
FROM EMPLOYEE
WHERE DATE_FORMAT(HIREDATE, '%d') < 15;
```

**Output:**
```
+--------+------------+
| ENAME  | HIREDATE   |
+--------+------------+
| JONES  | 1981-04-02 |
| BLAKE  | 1981-05-01 |
| CLARK  | 1981-06-09 |
| SCOTT  | 1982-12-09 |
| TURNER | 1981-09-08 |
| ADAMS  | 1983-01-12 |
| JAMES  | 1981-12-03 |
| FORD   | 1981-12-03 |
+--------+------------+
8 rows in set (0.001 sec)
```

---

### Problem 15: Display Employees Whose Joining DATE Is Available in DEPTNO

**Objective:** Find employees where the day-of-month from their hire date matches any existing department number.

```sql
SELECT ENAME, HIREDATE, DAY(HIREDATE) AS JOIN_DAY, DEPTNO
FROM EMPLOYEE
WHERE DAY(HIREDATE) IN (SELECT DEPTNO FROM DEPARTMENT);
```

**Explanation:** DEPARTMENT table has DEPTNO values: 10, 20, 30, 40. We check if the day portion of HIREDATE matches any of these values.

**Output:**
```
+-------+------------+----------+--------+
| ENAME | HIREDATE   | JOIN_DAY | DEPTNO |
+-------+------------+----------+--------+
| ALLEN | 1981-02-20 |       20 |     30 |
+-------+------------+----------+--------+
1 row in set (0.001 sec)
```
---

> **Submitted By:** shreyansh pratap mishra
> **Course:** DBMS Lab
