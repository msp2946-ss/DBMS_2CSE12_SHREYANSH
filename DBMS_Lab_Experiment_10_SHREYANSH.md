# <center>Experiment No.10
### Perform the following Query 
### 1. Display the names of employees from department number 10 with salary greater than that of any employee working in other departments. 
~~~sql
SELECT ENAME
FROM EMPLOYEE
WHERE DEPTNO = 10
AND SAL > ANY (
    SELECT SAL
    FROM EMPLOYEE
    WHERE DEPTNO <> 10
);
~~~
### 2. Display the names of employee from department number 10 with salary greater than that of all employee working in other departments. 
~~~sql
SELECT ENAME
FROM EMPLOYEE
WHERE DEPTNO = 10
AND SAL > ALL (
    SELECT SAL
    FROM EMPLOYEE
    WHERE DEPTNO <> 10
);
~~~
### 3. Display the details of employees who are in sales dept and grade is C.  (CORRECTION)
~~~sql
SELECT E.*
FROM EMPLOYEE E
JOIN DEPARTMENT D ON E.DEPTNO = D.DEPTNO
JOIN SALGRADE S ON E.SAL BETWEEN S.LOSAL AND S.HISAL
WHERE D.DNAME = 'SALES'
AND S.GRADE = 3;
~~~
### 4. Display those who are not managers and who manages anyone.  (CORRECTION)
~~~sql
SELECT ENAME
FROM EMPLOYEE
WHERE JOB <> 'MANAGER'
AND EMPNO IN (
    SELECT MGR FROM EMPLOYEE WHERE MGR IS NOT NULL
);
~~~
### 5. Display those employees whose manager name is jones. 
~~~sql
SELECT E.ENAME
FROM EMPLOYEE E
JOIN EMPLOYEE M ON E.MGR = M.EMPNO
WHERE M.ENAME = 'JONES';
~~~
### 6. Display ename who are working in sales dept. 
~~~sql
SELECT E.ENAME
FROM EMPLOYEE E
JOIN DEPARTMENT D ON E.DEPTNO = D.DEPTNO
WHERE D.DNAME = 'SALES';
~~~
### 7. Display employee name, deptname, salary and comm. For those sal in between 2000 to 5000 while location is Mumbai. (CORRECTION)
~~~sql
SELECT E.ENAME, D.DNAME, E.SAL, E.COMM
FROM EMPLOYEE E
JOIN DEPARTMENT D ON E.DEPTNO = D.DEPTNO
WHERE E.SAL BETWEEN 2000 AND 5000
AND D.LOC = 'MUMBAI';
~~~
### 8. Display those employees whose salary greater than his manager salary. 
~~~sql
SELECT E.ENAME
FROM EMPLOYEE E
JOIN EMPLOYEE M ON E.MGR = M.EMPNO
WHERE E.SAL > M.SAL;
~~~
### 9. Display those employees who are working in the same dept where his manager is working. 
~~~sql
SELECT E.ENAME
FROM EMPLOYEE E
JOIN EMPLOYEE M ON E.MGR = M.EMPNO
WHERE E.DEPTNO = M.DEPTNO;
~~~
### 10. Display grade and employees name for the dept no 10 or 30 but grade is not D, while joined the company before 31-dec-82. (CORRECTION)
~~~sql
SELECT E.ENAME, S.GRADE
FROM EMPLOYEE E
JOIN SALGRADE S ON E.SAL BETWEEN S.LOSAL AND S.HISAL
WHERE E.DEPTNO IN (10, 30)
AND S.GRADE <> D
AND E.HIREDATE < '1982-12-31';
