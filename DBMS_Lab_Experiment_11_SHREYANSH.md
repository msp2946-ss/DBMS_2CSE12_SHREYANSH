# <center>Experiment No.11
### Perform the following Query 
###  1. Delete those employees who joined the company before 31 dec-82 while there dept location is ‘new york’ or ‘chicago’. 
~~~sql
DELETE FROM EMPLOYEE
WHERE HIREDATE < '1982-12-31'
AND DEPTNO IN (
    SELECT DEPTNO
    FROM DEPARTMENT
    WHERE LOC IN ('NEW YORK', 'CHICAGO')
);
~~~
###  2. Display employee name, job, deptname, location for all who are working as managers. 
~~~sql
SELECT 
    E.ENAME,
    E.JOB,
    D.DNAME,
    D.LOC
FROM EMPLOYEE E
JOIN DEPARTMENT D 
ON E.DEPTNO = D.DEPTNO
WHERE E.JOB = 'MANAGER';
~~~
###  3. Display name and salary of ford if his sal is equal to high sal of his grade. 
~~~sql
SELECT E.ENAME, E.SAL
FROM EMPLOYEE E
JOIN SALGRADE S 
ON E.SAL BETWEEN S.LOSAL AND S.HISAL
WHERE E.ENAME = 'FORD'
AND E.SAL = (
    SELECT MAX(E2.SAL)
    FROM EMPLOYEE E2
    JOIN SALGRADE S2 
    ON E2.SAL BETWEEN S2.LOSAL AND S2.HISAL
    WHERE S2.GRADE = S.GRADE
);
~~~
###  4. Find out the top 5 earner of company. 
~~~sql
SELECT ENAME, SAL
FROM EMPLOYEE
ORDER BY SAL DESC
LIMIT 5;
~~~
###  5. Display the name of those employees who are getting highest salary. 
~~~sql
SELECT ENAME
FROM EMPLOYEE
WHERE SAL = (SELECT MAX(SAL) FROM EMPLOYEE);
~~~
###  6. Display those employees whose salary is equal to average of maximum and minimum. 
~~~sql
SELECT ENAME, SAL
FROM EMPLOYEE
WHERE SAL = (
    (SELECT MAX(SAL) FROM EMPLOYEE) +
    (SELECT MIN(SAL) FROM EMPLOYEE)
) / 2;
~~~
###  7. Display dname where at least 3 are working and display only dname 
~~~sql
SELECT D.DNAME
FROM DEPARTMENT D
JOIN EMPLOYEE E ON D.DEPTNO = E.DEPTNO
GROUP BY D.DNAME
HAVING COUNT(*) >= 3;
~~~
###  8. Display name of those managers names whose salary is more than average salary of company. 
~~~sql
SELECT ENAME
FROM EMPLOYEE
WHERE JOB = 'MANAGER'
AND SAL > (SELECT AVG(SAL) FROM EMPLOYEE);
~~~
###  9. Display those managers name whose salary is more than an average salary of his employees. 
~~~sql
SELECT M.ENAME
FROM EMPLOYEE M
WHERE M.JOB = 'MANAGER'
AND M.SAL > (
    SELECT AVG(E.SAL)
    FROM EMPLOYEE E
    WHERE E.MGR = M.EMPNO
);
~~~
###  10. Display employee name, sal, comm and net pay for those employees whose net pay are greater than or equal to any other employee salary of the company? 
~~~sql
SELECT ENAME, SAL, COMM,
       (SAL + IFNULL(COMM,0)) AS NET_PAY
FROM EMPLOYEE
WHERE (SAL + IFNULL(COMM,0)) >= ANY (
    SELECT SAL FROM EMPLOYEE
);
~~~
