# DBMS Lab Experiment – 1

## Study and Implementation of DDL & DML Commands

### (Employee–Department Database)

---

## Aim

To create and manipulate an Employee–Department database using DDL and DML commands in MySQL.

---

## Software / Tools Used

- **Database:** MySQL (MariaDB)
- **Interface:** XAMPP – MySQL Terminal
- **Operating System:** macOS
- **Editor:** Visual Studio Code

---

## Database Used

**Database Name:** `SHREYANSH`

---

## STEP 0: Start MySQL (XAMPP)

```bash
/Applications/XAMPP/xamppfiles/bin/mysql -u root
```

### STEP 1: Create and Use Database

```sql
CREATE DATABASE SHREYANSH;
USE SHREYANSH;
```

### STEP 2: Create Department Table

 ```sql
CREATE TABLE Department (
    DeptNo INT(2) PRIMARY KEY,
    Dname VARCHAR(15) NOT NULL
);
```

### STEP 3: Insert Records into Department

```sql
INSERT INTO Department VALUES
(10, 'RESEARCH'),
(20, 'ACCOUNTING'),
(30, 'SALES'),
(40, 'OPERATIONS');
```

```text
MariaDB [SHREYANSH]> SELECT * FROM DEPARTMENT;
+--------+------------+
| DEPTNO | DNAME      |
+--------+------------+
|     10 | RESEARCH   |
|     20 | ACCOUNTING |
|     30 | SALES      |
|     40 | OPERATIONS |
+--------+------------+
```

### Step 4

```sql
 MariaDB [SHREYANSH]> CREATE TABLE EMPLOYEE (
    ->     EMPNO INT(4) PRIMARY KEY,
    ->     ENAME VARCHAR(20) NOT NULL,
    ->     JOB VARCHAR(20),
    ->     MGR INT(4),
    ->     HIREDATE DATE,
    ->     SAL DECIMAL(10,2),
    ->     COMM DECIMAL(7,2),
    ->     DEPTNO INT(2),
    ->     FOREIGN KEY (DEPTNO) REFERENCES DEPARTMENT(DEPTNO)
```

### STEP 5: Insert Records into Employee

```sql
MariaDB [SHREYANSH]> INSERT INTO EMPLOYEE VALUES
    -> (7369,'SMITH','CLERK',7902,'1980-12-17',800,NULL,20),
    -> (7499,'ALLEN','SALESMAN',7698,'1981-02-20',1600,300,30),
    -> (7521,'WARD','SALESMAN',7698,'1981-02-22',1250,300,30),
    -> (7566,'JONES','MANAGER',7839,'1981-04-02',2975,NULL,20),
    -> (7654,'MARTIN','SALESMAN',7698,'1981-09-28',1250,1400,30),
    -> (7698,'BLAKE','MANAGER',7839,'1981-05-01',2850,NULL,30),
    -> (7782,'CLARK','MANAGER',7839,'1981-06-09',2450,NULL,20),
    -> (7788,'SCOTT','ANALYST',7566,'1982-12-09',3000,NULL,40),
    -> (7839,'KING','PRESIDENT',NULL,'1981-11-17',5000,NULL,20),
    -> (7844,'TURNER','SALESMAN',7698,'1981-09-08',1500,0,30),
    -> (7876,'ADAMS','CLERK',7788,'1983-01-12',1100,NULL,20),
    -> (7900,'JAMES','CLERK',7698,'1981-12-03',950,NULL,30),
    -> (7902,'FORD','ANALYST',7566,'1981-12-03',3000,NULL,20),
    -> (7934,'MILLER','CLERK',7782,'1982-01-23',1300,NULL,10);
```

```sql
SELECT * FROM Employee;
MariaDB [SHREYANSH]> SELECT * FROM EMPLOYEE_MASTER;
```

```text
+-------+--------+-----------+------+------------+---------+---------+--------+
| EMPNO | ENAME  | JOB       | MGR  | HIREDATE   | SAL     | COMM    | DEPTNO |
+-------+--------+-----------+------+------------+---------+---------+--------+
|  7369 | SMITH  | CLERK     | 7902 | 1980-12-17 |  800.00 |    NULL |     20 |
|  7499 | ALLEN  | SALESMAN  | 7698 | 1981-02-20 | 1600.00 |  300.00 |     30 |
|  7521 | WARD   | SALESMAN  | 7698 | 1981-02-22 | 1250.00 |  300.00 |     30 |
|  7566 | JONES  | MANAGER   | 7839 | 1981-04-02 | 2975.00 |    NULL |     20 |
|  7654 | MARTIN | SALESMAN  | 7698 | 1981-09-28 | 1250.00 | 1400.00 |     30 |
|  7698 | BLAKE  | MANAGER   | 7839 | 1981-05-01 | 2850.00 |    NULL |     30 |
|  7782 | CLARK  | MANAGER   | 7839 | 1981-06-09 | 2450.00 |    NULL |     20 |
|  7788 | SCOTT  | ANALYST   | 7566 | 1982-12-09 | 3000.00 |    NULL |     40 |
|  7839 | KING   | PRESIDENT | NULL | 1981-11-17 | 5000.00 |    NULL |     20 |
|  7844 | TURNER | SALESMAN  | 7698 | 1981-09-08 | 1500.00 |    0.00 |     30 |
|  7876 | ADAMS  | CLERK     | 7788 | 1983-01-12 | 1100.00 |    NULL |     20 |
|  7900 | JAMES  | CLERK     | 7698 | 1981-12-03 |  950.00 |    NULL |     30 |
|  7902 | FORD   | ANALYST   | 7566 | 1981-12-03 | 3000.00 |    NULL |     20 |
|  7934 | MILLER | CLERK     | 7782 | 1982-01-23 | 1300.00 |    NULL |     10 |
+-------+--------+-----------+------+------------+---------+---------+--------+
```

## Lab Queries

### 1. Create Employee_master Table

```sql
MariaDB [SHREYANSH]> SELECT * FROM Employee;
CREATE TABLE Employee_master AS
SELECT * FROM Employee;
```

```text
MariaDB [SHREYANSH]> SELECT * FROM EMPLOYEE_MASTER;
+-------+--------+-----------+------+------------+---------+---------+--------+
| EMPNO | ENAME  | JOB       | MGR  | HIREDATE   | SAL     | COMM    | DEPTNO |
+-------+--------+-----------+------+------------+---------+---------+--------+
|  7369 | SMITH  | CLERK     | 7902 | 1980-12-17 |  800.00 |    NULL |     20 |
|  7499 | ALLEN  | SALESMAN  | 7698 | 1981-02-20 | 1600.00 |  300.00 |     30 |
|  7521 | WARD   | SALESMAN  | 7698 | 1981-02-22 | 1250.00 |  300.00 |     30 |
|  7566 | JONES  | MANAGER   | 7839 | 1981-04-02 | 2975.00 |    NULL |     20 |
|  7654 | MARTIN | SALESMAN  | 7698 | 1981-09-28 | 1250.00 | 1400.00 |     30 |
|  7698 | BLAKE  | MANAGER   | 7839 | 1981-05-01 | 2850.00 |    NULL |     30 |
|  7782 | CLARK  | MANAGER   | 7839 | 1981-06-09 | 2450.00 |    NULL |     20 |
|  7788 | SCOTT  | ANALYST   | 7566 | 1982-12-09 | 3000.00 |    NULL |     40 |
|  7839 | KING   | PRESIDENT | NULL | 1981-11-17 | 5000.00 |    NULL |     20 |
|  7844 | TURNER | SALESMAN  | 7698 | 1981-09-08 | 1500.00 |    0.00 |     30 |
|  7876 | ADAMS  | CLERK     | 7788 | 1983-01-12 | 1100.00 |    NULL |     20 |
|  7900 | JAMES  | CLERK     | 7698 | 1981-12-03 |  950.00 |    NULL |     30 |
|  7902 | FORD   | ANALYST   | 7566 | 1981-12-03 | 3000.00 |    NULL |     20 |
+-------+--------+-----------+------+------------+---------+---------+--------+
```

### 2. Delete Employees from DeptNo = 10

```sql
DELETE FROM Employee_master
WHERE DeptNo = 10;
```

```text
MariaDB [SHREYANSH]> SELECT * FROM EMPLOYEE_MASTER;
+-------+--------+-----------+------+------------+---------+---------+--------+
| EMPNO | ENAME  | JOB       | MGR  | HIREDATE   | SAL     | COMM    | DEPTNO |
+-------+--------+-----------+------+------------+---------+---------+--------+
|  7369 | SMITH  | CLERK     | 7902 | 1980-12-17 |  800.00 |    NULL |     20 |
|  7499 | ALLEN  | SALESMAN  | 7698 | 1981-02-20 | 1600.00 |  300.00 |     30 |
|  7521 | WARD   | SALESMAN  | 7698 | 1981-02-22 | 1250.00 |  300.00 |     30 |
|  7566 | JONES  | MANAGER   | 7839 | 1981-04-02 | 2975.00 |    NULL |     20 |
|  7654 | MARTIN | SALESMAN  | 7698 | 1981-09-28 | 1250.00 | 1400.00 |     30 |
|  7698 | BLAKE  | MANAGER   | 7839 | 1981-05-01 | 2850.00 |    NULL |     30 |
|  7782 | CLARK  | MANAGER   | 7839 | 1981-06-09 | 2450.00 |    NULL |     20 |
|  7788 | SCOTT  | ANALYST   | 7566 | 1982-12-09 | 3000.00 |    NULL |     40 |
|  7839 | KING   | PRESIDENT | NULL | 1981-11-17 | 5000.00 |    NULL |     20 |
|  7844 | TURNER | SALESMAN  | 7698 | 1981-09-08 | 1500.00 |    0.00 |     30 |
|  7876 | ADAMS  | CLERK     | 7788 | 1983-01-12 | 1100.00 |    NULL |     20 |
|  7900 | JAMES  | CLERK     | 7698 | 1981-12-03 |  950.00 |    NULL |     30 |
|  7902 | FORD   | ANALYST   | 7566 | 1981-12-03 | 3000.00 |    NULL |     20 |
+-------+--------+-----------+------+------------+---------+---------+--------+
```

### 3. Increase Salary by 10% for DeptNo = 20

```sql
MariaDB [SHREYANSH]> UPDATE EMPLOYEE_MASTER
    -> SET SAL = SAL + (SAL * 0.10)
    -> WHERE DEPTNO = 20;
```

```text
MariaDB [SHREYANSH]> SELECT EMPNO, ENAME, SAL, DEPTNO
    -> FROM EMPLOYEE_MASTER
    -> WHERE DEPTNO = 20;
+-------+-------+---------+--------+
| EMPNO | ENAME | SAL     | DEPTNO |
+-------+-------+---------+--------+
|  7369 | SMITH |  880.00 |     20 |
|  7566 | JONES | 3272.50 |     20 |
|  7782 | CLARK | 2695.00 |     20 |
|  7839 | KING  | 5500.00 |     20 |
|  7876 | ADAMS | 1210.00 |     20 |
|  7902 | FORD  | 3300.00 |     20 |
+-------+-------+---------+--------+
```

### 4. Modify Salary Column Size

```sql
ALTER TABLE Employee_master
MODIFY Sal DECIMAL(10,2);
```

```text
MariaDB [SHREYANSH]> DESC EMPLOYEE_MASTER;
+----------+---------------+------+-----+---------+-------+
| Field    | Type          | Null | Key | Default | Extra |
+----------+---------------+------+-----+---------+-------+
| EMPNO    | int(4)        | NO   |     | NULL    |       |
| ENAME    | varchar(20)   | NO   |     | NULL    |       |
| JOB      | varchar(20)   | YES  |     | NULL    |       |
| MGR      | int(4)        | YES  |     | NULL    |       |
| HIREDATE | date          | YES  |     | NULL    |       |
| SAL      | decimal(10,2) | YES  |     | NULL    |       |
| COMM     | decimal(7,2)  | YES  |     | NULL    |       |
| DEPTNO   | int(2)        | YES  |     | NULL    |       |
+----------+---------------+------+-----+---------+-------+
```

### 5. Drop Employee_master Table

```sql
DROP TABLE Employee_master;
```

```text
MariaDB [SHREYANSH]> SHOW TABLES;
+------------------+
| Tables_in_SHREYANSH |
+------------------+
| DEPARTMENT       |
| EMPLOYEE         |
+------------------+
```

## Performing Queries Using Employee Table (Retrieving Data)

### Query 1: List all distinct jobs in Employee

```sql
SELECT DISTINCT Job
FROM Employee;
```

```text
MariaDB [SHREYANSH]> SELECT DISTINCT JOB
    -> FROM EMPLOYEE;
+-----------+
| JOB       |
+-----------+
| CLERK     |
| SALESMAN  |
| MANAGER   |
| ANALYST   |
| PRESIDENT |
+-----------+
```

### Query 2: List all information about employees in Department Number 30

```sql
SELECT *
FROM Employee
WHERE DEPTNO = 30;
```

```text
MariaDB [SHREYANSH]> SELECT *
    -> FROM EMPLOYEE
    -> WHERE DEPTNO = 30;
+-------+--------+----------+------+------------+---------+---------+--------+
| EMPNO | ENAME  | JOB      | MGR  | HIREDATE   | SAL     | COMM    | DEPTNO |
+-------+--------+----------+------+------------+---------+---------+--------+
|  7499 | ALLEN  | SALESMAN | 7698 | 1981-02-20 | 1600.00 |  300.00 |     30 |
|  7521 | WARD   | SALESMAN | 7698 | 1981-02-22 | 1250.00 |  300.00 |     30 |
|  7654 | MARTIN | SALESMAN | 7698 | 1981-09-28 | 1250.00 | 1400.00 |     30 |  
|  7698 | BLAKE  | MANAGER  | 7839 | 1981-05-01 | 2850.00 |    NULL |     30 |
|  7844 | TURNER | SALESMAN | 7698 | 1981-09-08 | 1500.00 |    0.00 |     30 |
|  7900 | JAMES  | CLERK    | 7698 | 1981-12-03 |  950.00 |    NULL |     30 |
+-------+--------+----------+------+------------+---------+---------+--------+
```

### Query 3: Find department numbers with department names where DeptNo > 20

```sql
SELECT DeptNo, Dname
FROM Department
WHERE DeptNo > 20;
```

```text
MariaDB [SHREYANSH]> SELECT DEPTNO, DNAME
    -> FROM DEPARTMENT
    -> WHERE DEPTNO > 20;
+--------+------------+
| DEPTNO | DNAME      |
+--------+------------+
|     30 | SALES      |
|     40 | OPERATIONS |
+--------+------------+
```

### Query 4: Find all information about managers as well as clerks in Department 30

```sql
SELECT *
FROM Employee
WHERE DeptNo = 30
AND (Job = 'MANAGER' OR Job = 'CLERK');
```

```text
MariaDB [SHREYANSH]> SELECT *
    -> FROM EMPLOYEE
    -> WHERE DEPTNO = 30
    ->   AND (JOB = 'MANAGER' OR JOB = 'CLERK');
+-------+-------+---------+------+------------+---------+------+--------+
| EMPNO | ENAME | JOB     | MGR  | HIREDATE   | SAL     | COMM | DEPTNO |
+-------+-------+---------+------+------------+---------+------+--------+
|  7698 | BLAKE | MANAGER | 7839 | 1981-05-01 | 2850.00 | NULL |     30 |
|  7900 | JAMES | CLERK   | 7698 | 1981-12-03 |  950.00 | NULL |     30 |
+-------+-------+---------+------+------------+---------+------+--------+
```

### Query 5: List employee name, employee number and department of all clerks

```sql

SELECT Ename, EmpNo, DeptNo
FROM Employee
WHERE Job = 'CLERK';
```

```text
MariaDB [SHREYANSH]> SELECT ENAME, EMPNO, DEPTNO
    -> FROM EMPLOYEE
    -> WHERE JOB = 'CLERK';
+--------+-------+--------+
| ENAME  | EMPNO | DEPTNO |
+--------+-------+--------+
| SMITH  |  7369 |     20 |
| ADAMS  |  7876 |     20 |
| JAMES  |  7900 |     30 |
| MILLER |  7934 |     10 |
+--------+-------+--------+
```

### Query 6: Find all managers not in Department 30

```sql
SELECT *
FROM Employee
WHERE Job = 'MANAGER'
AND DeptNo <> 30;
```

```text
MariaDB [SHREYANSH]> SELECT *
    -> FROM EMPLOYEE
    -> WHERE JOB = 'MANAGER'
    ->   AND DEPTNO <> 30;
+-------+-------+---------+------+------------+---------+------+--------+
| EMPNO | ENAME | JOB     | MGR  | HIREDATE   | SAL     | COMM | DEPTNO |
+-------+-------+---------+------+------------+---------+------+--------+
|  7566 | JONES | MANAGER | 7839 | 1981-04-02 | 2975.00 | NULL |     20 |
|  7782 | CLARK | MANAGER | 7839 | 1981-06-09 | 2450.00 | NULL |     20 |
+-------+-------+---------+------+------------+---------+------+--------+
```

### Query 7: List information about employees in Department 10 who are not managers or clerks

```sql

SELECT *
FROM Employee
WHERE DeptNo = 10
AND Job NOT IN ('MANAGER', 'CLERK');
```

MariaDB [SHREYANSH]> SELECT *
    -> FROM EMPLOYEE
    -> WHERE DEPTNO = 10
    ->   AND JOB NOT IN ('MANAGER', 'CLERK');

### Query 8: Find employees and jobs earning between 1200 and 1400

```sql
SELECT Ename, Job, Sal
FROM Employee
WHERE Sal BETWEEN 1200 AND 1400;
```

```text
MariaDB [SHREYANSH]> SELECT ENAME, JOB, SAL
    -> FROM EMPLOYEE
    -> WHERE SAL BETWEEN 1200 AND 1400;
+--------+----------+---------+
| ENAME  | JOB      | SAL     |
+--------+----------+---------+
| WARD   | SALESMAN | 1250.00 |
| MARTIN | SALESMAN | 1250.00 |
| MILLER | CLERK    | 1300.00 |
+--------+----------+---------+
```

### Query 9: List name and department number of employees who are clerks, analysts or salesmen

```sql
SELECT Ename, DeptNo
FROM Employee
WHERE Job IN ('CLERK', 'ANALYST', 'SALESMAN');
```

```text
MariaDB [SHREYANSH]> SELECT ENAME, DEPTNO
    -> FROM EMPLOYEE
    -> WHERE JOB IN ('CLERK', 'ANALYST', 'SALESMAN');
+--------+--------+
| ENAME  | DEPTNO |
+--------+--------+
| SMITH  |     20 |
| ALLEN  |     30 |
| WARD   |     30 |
| MARTIN |     30 |
| SCOTT  |     40 |
| TURNER |     30 |
| ADAMS  |     20 |
| JAMES  |     30 |
| FORD   |     20 |
| MILLER |     10 |
+--------+--------+
```

### Query 10: List name and department number of employees whose names begin with ‘M’

```sql
SELECT Ename, DeptNo
FROM Employee
WHERE Ename LIKE 'M%';
```

```text
MariaDB [SHREYANSH]> SELECT ENAME, DEPTNO
    -> FROM EMPLOYEE
    -> WHERE ENAME LIKE 'M%';
+--------+--------+
| ENAME  | DEPTNO |
+--------+--------+
| MARTIN |     30 |
| MILLER |     10 |
+--------+--------+
```

## The above queries retrieve data from the Employee and Department tables using SELECT statements and its clauses such as WHERE, DISTINCT, IN, BETWEEN and LIKE

---
---
---

## STEP 0 — RESTORE ALL 14 RECORDS (BASE STATE)

```sql
SELECT * FROM EMPLOYEE;
```

### QUERY 1: List all distinct jobs in Employee

```sql
SELECT DISTINCT JOB
FROM Employee;
```

```text
MariaDB [SHREYANSH]> SELECT DISTINCT JOB
    -> FROM EMPLOYEE;
+-----------+
| JOB       |
+-----------+
| CLERK     |
| SALESMAN  |
| MANAGER   |
| ANALYST   |
| PRESIDENT |
+-----------+
```

### QUERY 2: List all information about employee in Department Number 30

```sql
SELECT *
FROM Employee
WHERE DEPTNO = 30;
```

```text
MariaDB [SHREYANSH]> SELECT *Vv
    -> FROM EMPLOYEE
    -> WHERE DEPTNO = 30;
+-------+--------+----------+------+------------+---------+---------+--------+
| EMPNO | ENAME  | JOB      | MGR  | HIREDATE   | SAL     | COMM    | DEPTNO |
+-------+--------+----------+------+------------+---------+---------+--------+
|  7499 | ALLEN  | SALESMAN | 7698 | 1981-02-20 | 1600.00 |  300.00 |     30 |
|  7521 | WARD   | SALESMAN | 7698 | 1981-02-22 | 1250.00 |  300.00 |     30 |
|  7654 | MARTIN | SALESMAN | 7698 | 1981-09-28 | 1250.00 | 1400.00 |     30 |
|  7698 | BLAKE  | MANAGER  | 7839 | 1981-05-01 | 2850.00 |    NULL |     30 |
|  7844 | TURNER | SALESMAN | 7698 | 1981-09-08 | 1500.00 |    0.00 |     30 |
|  7900 | JAMES  | CLERK    | 7698 | 1981-12-03 |  950.00 |    NULL |     30 |
+-------+--------+----------+------+------------+---------+---------+--------+
```

### QUERY 3: Find department number with department names greater than 20

```sql
SELECT DEPTNO, DNAME
FROM Department
WHERE DEPTNO > 20;
```

```text
MariaDB [SHREYANSH]> SELECT DEPTNO, DNAME
    -> FROM DEPARTMENT
    -> WHERE DEPTNO > 20;
+--------+------------+
| DEPTNO | DNAME      |
+--------+------------+
|     30 | SALES      |
|     40 | OPERATIONS |
+--------+------------+
```

### QUERY 4: Find all managers as well as clerks in department 30

```sql
SELECT *
FROM Employee
WHERE DEPTNO = 30
AND JOB IN ('MANAGER', 'CLERK');
```

```text
MariaDB [SHREYANSH]> SELECT *
    -> FROM EMPLOYEE
    -> WHERE DEPTNO = 30
    -> AND (JOB = 'MANAGER' OR JOB = 'CLERK');
+-------+-------+---------+------+------------+---------+------+--------+
| EMPNO | ENAME | JOB     | MGR  | HIREDATE   | SAL     | COMM | DEPTNO |
+-------+-------+---------+------+------------+---------+------+--------+
|  7698 | BLAKE | MANAGER | 7839 | 1981-05-01 | 2850.00 | NULL |     30 |
|  7900 | JAMES | CLERK   | 7698 | 1981-12-03 |  950.00 | NULL |     30 |
+-------+-------+---------+------+------------+---------+------+--------+
```

### QUERY 5: List employee name, employee number and department of all clerks

```sql
SELECT EMPNO, ENAME, DEPTNO
FROM Employee
WHERE JOB = 'CLERK';
```

```text
MariaDB [SHREYANSH]> SELECT EMPNO, ENAME, DEPTNO
    -> FROM EMPLOYEE
    -> WHERE JOB = 'CLERK';
+-------+--------+--------+
| EMPNO | ENAME  | DEPTNO |
+-------+--------+--------+
|  7369 | SMITH  |     20 |
|  7876 | ADAMS  |     20 |
|  7900 | JAMES  |     30 |
|  7934 | MILLER |     10 |
+-------+--------+--------+
```

### QUERY 6: Find all managers not in department 30

```sql
SELECT *
FROM Employee
WHERE JOB = 'MANAGER'
AND DEPTNO <> 30;
```

```text
MariaDB [SHREYANSH]> SELECT *
    -> FROM EMPLOYEE
    -> WHERE JOB = 'MANAGER'
    -> AND DEPTNO <> 30;
+-------+-------+---------+------+------------+---------+------+--------+
| EMPNO | ENAME | JOB     | MGR  | HIREDATE   | SAL     | COMM | DEPTNO |
+-------+-------+---------+------+------------+---------+------+--------+
|  7566 | JONES | MANAGER | 7839 | 1981-04-02 | 2975.00 | NULL |     20 |
|  7782 | CLARK | MANAGER | 7839 | 1981-06-09 | 2450.00 | NULL |     20 |
+-------+-------+---------+------+------------+---------+------+--------+
```

### QUERY 7: Employees in department 10 who are not manager or clerk

```sql
SELECT *
FROM Employee
WHERE DEPTNO = 10
AND JOB NOT IN ('MANAGER', 'CLERK');
```

MariaDB [SHREYANSH]> SELECT *
    -> FROM EMPLOYEE
    -> WHERE DEPTNO = 10
    -> AND JOB NOT IN ('MANAGER','CLERK');

### QUERY 8: Employees and jobs earning between 1200 and 1400

```sql
SELECT ENAME, JOB, SAL
FROM Employee
WHERE SAL BETWEEN 1200 AND 1400;
```

```text
MariaDB [SHREYANSH]> SELECT ENAME, JOB, SAL
    -> FROM EMPLOYEE
    -> WHERE SAL BETWEEN 1200 AND 1400;
+--------+----------+---------+
| ENAME  | JOB      | SAL     |
+--------+----------+---------+
| WARD   | SALESMAN | 1250.00 |
| MARTIN | SALESMAN | 1250.00 |
| MILLER | CLERK    | 1300.00 |
+--------+----------+---------+
```

### QUERY 9: Name and department number of clerks, analysts or salesman

```sql
SELECT ENAME, DEPTNO
FROM Employee
WHERE JOB IN ('CLERK', 'ANALYST', 'SALESMAN');
```

```text
MariaDB [SHREYANSH]> SELECT ENAME, DEPTNO
    -> FROM EMPLOYEE
    -> WHERE JOB IN ('CLERK','ANALYST','SALESMAN');
+--------+--------+
| ENAME  | DEPTNO |
+--------+--------+
| SMITH  |     20 |
| ALLEN  |     30 |
| WARD   |     30 |
| MARTIN |     30 |
| SCOTT  |     40 |
| TURNER |     30 |
| ADAMS  |     20 |
| JAMES  |     30 |
| FORD   |     20 |
| MILLER |     10 |
+--------+--------+  
```

### QUERY 10: Name and department number of employees whose names begin with M

```sql
SELECT ENAME, DEPTNO
FROM Employee
WHERE ENAME LIKE 'M%';
```

```text
MariaDB [SHREYANSH]> SELECT ENAME, DEPTNO
    -> FROM EMPLOYEE
    -> WHERE ENAME LIKE 'M%';
+--------+--------+
| ENAME  | DEPTNO |
+--------+--------+
| MARTIN |     30 |
| MILLER |     10 |
+--------+--------+
```
