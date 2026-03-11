# Part 2 – Schema Design & Table Creation

```sql
CREATE TABLE Department (
    Deptcode VARCHAR(10) PRIMARY KEY,
    Deptlocation VARCHAR(100) NOT NULL
);

CREATE TABLE Employee (
    Empno INT PRIMARY KEY,
    Name VARCHAR(120) NOT NULL,
    Job VARCHAR(120) NOT NULL,
    Hiredate DATE NOT NULL,
    Salary DECIMAL(12,2) NOT NULL,
    Deptcode VARCHAR(10) NOT NULL,
    CONSTRAINT fk_employee_department
        FOREIGN KEY (Deptcode) REFERENCES Department(Deptcode)
);
```
