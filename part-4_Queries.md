# Part 4 - Required SQL Queries

## 1. Average and Total Salary

```sql
SELECT
    ROUND(AVG(Salary), 2) AS AverageSalary,
    ROUND(SUM(Salary), 2) AS TotalSalary
FROM employee;
```

## 2. Count Employees in a Department

```sql
SELECT
    Deptcode,
    COUNT(*) AS EmployeeCount
FROM employee
WHERE Deptcode = 'D10'
GROUP BY Deptcode;
```

## 3. Name Pattern Search
Find employees whose names start with `A` and are at least 4 characters long.

```sql
SELECT
    Empno,
    Name,
    Job,
    Deptcode
FROM employee
WHERE Name LIKE 'A%'
  AND CHAR_LENGTH(Name) >= 4
ORDER BY Name;
```

## 4. Employees by Job Title
Chosen job title: `Data Analyst`

```sql
SELECT
    Empno,
    Name,
    Job,
    Hiredate,
    Salary,
    Deptcode
FROM employee
WHERE Job = 'Data Analyst'
ORDER BY Name;
```

## 5. Employees Hired Between Two Dates
Chosen range: `2018-01-01` to `2020-12-31`

```sql
SELECT
    Empno,
    Name,
    Job,
    Hiredate,
    Salary,
    Deptcode
FROM employee
WHERE Hiredate BETWEEN '2018-01-01' AND '2020-12-31'
ORDER BY Name;
```

## 6. Min and Max Salary

```sql
SELECT
    MIN(Salary) AS MinSalary,
    MAX(Salary) AS MaxSalary
FROM employee;
```

## 7. Earliest and Latest Hire Date

```sql
SELECT
    MIN(Hiredate) AS EarliestHireDate,
    MAX(Hiredate) AS LatestHireDate
FROM employee;
```

## 8. Employee Count per Department
(Using `Deptlocation` as department descriptor)

```sql
SELECT
    d.Deptcode,
    d.Deptlocation,
    COUNT(e.Empno) AS EmployeeCount
FROM department d
LEFT JOIN employee e ON e.Deptcode = d.Deptcode
GROUP BY d.Deptcode, d.Deptlocation
ORDER BY d.Deptcode;
```

## 9. Average Salary per Department

```sql
SELECT
    d.Deptcode,
    d.Deptlocation,
    ROUND(AVG(e.Salary), 2) AS `Average Salary`
FROM department d
LEFT JOIN employee e ON e.Deptcode = d.Deptcode
GROUP BY d.Deptcode, d.Deptlocation
ORDER BY d.Deptcode;
```

## 10. High-Salary Departments
Threshold chosen: total salary greater than `70000`

```sql
SELECT
    d.Deptcode,
    d.Deptlocation,
    ROUND(SUM(e.Salary), 2) AS TotalDepartmentSalary
FROM department d
JOIN employee e ON e.Deptcode = d.Deptcode
GROUP BY d.Deptcode, d.Deptlocation
HAVING SUM(e.Salary) > 70000
ORDER BY TotalDepartmentSalary DESC;
```

## 11. Employees in a Location
Chosen location: `Vancouver`

```sql
SELECT
    e.Empno,
    e.Name,
    e.Job,
    e.Hiredate,
    e.Salary,
    d.Deptcode,
    d.Deptlocation
FROM employee e
JOIN department d ON d.Deptcode = e.Deptcode
WHERE d.Deptlocation = 'Vancouver'
ORDER BY e.Name;
```

## 12. Total Salary by Department and Job Title

```sql
SELECT
    d.Deptcode,
    d.Deptlocation,
    e.Job,
    ROUND(SUM(e.Salary), 2) AS TotalSalary
FROM employee e
JOIN department d ON d.Deptcode = e.Deptcode
GROUP BY d.Deptcode, d.Deptlocation, e.Job
ORDER BY d.Deptcode, e.Job;
```
