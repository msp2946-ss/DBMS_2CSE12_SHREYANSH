# <center>Experiment No.9
### Perform the following Query 
### 1. Display the name of emp name who earns highest salary. 
~~~sql
SELECT ENAME
FROM EMPLOYEE
WHERE SAL = (SELECT MAX(SAL) FROM EMPLOYEE);
~~~
### 2. Display the employee number and name of employee working as clerk and earning highest salary among clerks. 
~~~sql
SELECT EMPNO, ENAME
FROM EMPLOYEE
WHERE JOB = 'CLERK'
AND SAL = (
    SELECT MAX(SAL)
    FROM EMPLOYEE
    WHERE JOB = 'CLERK'
);
~~~
### 3. Display the names of the salesman who earns a salary more than the highest salary of any clerk. 
~~~sql
SELECT ENAME
FROM EMPLOYEE
WHERE JOB = 'SALESMAN'
AND SAL > (
    SELECT MAX(SAL)
    FROM EMPLOYEE
    WHERE JOB = 'CLERK'
);
~~~
### 4. Display the names of clerks who earn salary more than that of james of that of sal lesser than that of scott.
~~~sql
SELECT ENAME
FROM EMPLOYEE
WHERE JOB = 'CLERK'
AND SAL > (
    SELECT SAL FROM EMPLOYEE WHERE ENAME = 'JAMES'
)
AND SAL < (
    SELECT SAL FROM EMPLOYEE WHERE ENAME = 'SCOTT'
);
~~~
### 5. Display the names of employees who earn a sal more than that of james or that of salary greater than that of scott.
~~~sql
SELECT ENAME
FROM EMPLOYEE
WHERE SAL > (
    SELECT SAL FROM EMPLOYEE WHERE ENAME = 'JAMES'
)
OR SAL > (
    SELECT SAL FROM EMPLOYEE WHERE ENAME = 'SCOTT'
);
~~~
### 6. Display the names of the employees who earn highest salary in their respective departments. 
~~~sql
SELECT ENAME, DEPTNO, SAL
FROM EMPLOYEE E
WHERE SAL = (
    SELECT MAX(SAL)
    FROM EMPLOYEE
    WHERE DEPTNO = E.DEPTNO
);
~~~
### 7. Display the names of employees who earn highest salaries in their respective job groups. 
~~~sql
SELECT ENAME, JOB, SAL
FROM EMPLOYEE E
WHERE SAL = (
    SELECT MAX(SAL)
    FROM EMPLOYEE
    WHERE JOB = E.JOB
);
~~~
### 8. Display the employee names who are working in accounting dept. 
~~~sql
SELECT ENAME
FROM EMPLOYEE
WHERE DEPTNO = (
    SELECT DEPTNO
    FROM DEPARTMENT
    WHERE DNAME = 'ACCOUNTING'
);
~~~
### 9. Display the employee names who are working in Mumbai. 
~~~sql
SELECT ENAME
FROM EMPLOYEE
WHERE DEPTNO = (
    SELECT DEPTNO
    FROM DEPARTMENT
    WHERE LOC = 'MUMBAI'
);
~~~
### 10. Display the job groups having total salary greater than the maximum salary for managers. 
~~~sql
SELECT JOB, SUM(SAL) AS TOTAL_SALARY
FROM EMPLOYEE
GROUP BY JOB
HAVING SUM(SAL) > (
    SELECT MAX(SAL)
    FROM EMPLOYEE
    WHERE JOB = 'MANAGER'
);
~~~
