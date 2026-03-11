# Part 3 – Data Insertion

## 1. Populate Data

```sql
INSERT INTO department (Deptcode, Deptlocation) VALUES
('D01', 'Vancouver'),
('D02', 'Seattle'),
('D03', 'Portland'),
('D04', 'San Francisco'),
('D05', 'Los Angeles'),
('D06', 'San Diego'),
('D07', 'Phoenix'),
('D08', 'Denver'),
('D09', 'Dallas'),
('D10', 'Austin'),
('D11', 'Houston'),
('D12', 'Chicago'),
('D13', 'Detroit'),
('D14', 'Miami'),
('D15', 'Orlando'),
('D16', 'Atlanta'),
('D17', 'Charlotte'),
('D18', 'Washington'),
('D19', 'Boston'),
('D20', 'New York'),
('D21', 'Philadelphia'),
('D22', 'Newark'),
('D23', 'Toronto'),
('D24', 'Montreal'),
('D25', 'Calgary'),
('D26', 'Edmonton'),
('D27', 'Winnipeg'),
('D28', 'Ottawa'),
('D29', 'Quebec City'),
('D30', 'Halifax');
```

```sql
INSERT INTO employee (Empno, Name, Job, Hiredate, Salary, Deptcode) VALUES
(3001, 'Liam Carter', 'Software Engineer', '2019-01-15', 72000.00, 'D01'),
(3002, 'Emma Brooks', 'Data Analyst', '2018-03-22', 68000.00, 'D02'),
(3003, 'Noah Bennett', 'Accountant', '2020-07-10', 61000.00, 'D03'),
(3004, 'Olivia Hayes', 'HR Specialist', '2017-11-05', 59000.00, 'D04'),
(3005, 'William Price', 'Marketing Coordinator', '2021-02-18', 55000.00, 'D05'),
(3006, 'Ava Simmons', 'Project Manager', '2016-09-12', 83000.00, 'D06'),
(3007, 'James Turner', 'Sales Executive', '2019-06-01', 64000.00, 'D07'),
(3008, 'Sophia Reed', 'UX Designer', '2022-04-14', 70000.00, 'D08'),
(3009, 'Benjamin Ward', 'Systems Administrator', '2015-12-03', 76000.00, 'D09'),
(3010, 'Isabella Cox', 'Business Analyst', '2020-10-19', 69000.00, 'D10'),
(3011, 'Lucas Kelly', 'QA Engineer', '2018-08-27', 65000.00, 'D11'),
(3012, 'Mia Foster', 'DevOps Engineer', '2017-05-30', 87000.00, 'D12'),
(3013, 'Henry Powell', 'Financial Analyst', '2019-09-09', 67000.00, 'D13'),
(3014, 'Amelia Long', 'Recruiter', '2021-01-25', 56000.00, 'D14'),
(3015, 'Alexander Ross', 'Customer Support Lead', '2016-04-11', 58000.00, 'D15'),
(3016, 'Harper Diaz', 'Product Owner', '2018-12-17', 91000.00, 'D16'),
(3017, 'Daniel Myers', 'Network Engineer', '2017-07-21', 74000.00, 'D17'),
(3018, 'Evelyn Murphy', 'Content Strategist', '2022-06-06', 60000.00, 'D18'),
(3019, 'Matthew Hughes', 'Operations Manager', '2015-03-29', 88000.00, 'D19'),
(3020, 'Abigail Bell', 'Compliance Officer', '2020-11-13', 71000.00, 'D20'),
(3021, 'Joseph Bennett', 'Database Administrator', '2019-02-07', 82000.00, 'D21'),
(3022, 'Emily Richardson', 'Procurement Specialist', '2018-10-01', 63000.00, 'D22'),
(3023, 'David Sanders', 'Security Analyst', '2021-05-16', 73000.00, 'D23'),
(3024, 'Ella Perry', 'Payroll Specialist', '2016-01-20', 62000.00, 'D24'),
(3025, 'Michael Jenkins', 'Frontend Developer', '2022-09-09', 69000.00, 'D25'),
(3026, 'Scarlett Coleman', 'Backend Developer', '2019-04-02', 78000.00, 'D26'),
(3027, 'Christopher Patterson', 'Technical Writer', '2017-02-14', 57000.00, 'D27'),
(3028, 'Grace Howard', 'Office Administrator', '2018-07-07', 54000.00, 'D28'),
(3029, 'Andrew Bryant', 'Legal Assistant', '2020-08-24', 61000.00, 'D29'),
(3030, 'Chloe Russell', 'Data Scientist', '2021-12-01', 95000.00, 'D30');
```


## 2. Documented SELECTs

### `department`

```sql
SELECT Deptcode, Deptlocation
FROM department
ORDER BY Deptcode;
```

```sql
SELECT Deptcode, Deptlocation
FROM department
WHERE Deptcode BETWEEN 'D10' AND 'D20'
ORDER BY Deptcode;
```

### `employee`

```sql
SELECT Empno, Name, Job, Salary, Deptcode
FROM employee
ORDER BY Empno;
```

```sql
SELECT Empno, Name, Salary, Deptcode
FROM employee
WHERE Salary >= 80000
ORDER BY Salary DESC;
```
