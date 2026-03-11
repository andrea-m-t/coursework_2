# Part 1 - Normalization up to 3NF

## 1. Raw dataset - Denormalized table

| Empno | Deptcode | Deptlocation     | Name             | Job                    | Hiredate   | Salary    |
|------:|:--------:|------------------|------------------|------------------------|------------|----------:|
| 1001  | 3D       | Sidokumpul       | Benjamin Miguet  | Programmer IV          | 2019-10-25 | 133608.91 |
| 1002  | 1C       | Pointe-a-Pitre   | Biddy Coppock    | Health Coach III       | 2016-12-09 | 135302.24 |
| 1003  | 4B       | Lilla Edet       | Desmond Ogbourne | Senior Cost Accountant | 2020-03-24 | 55991.73  |
| 1004  | 1A       | Nemery           | Marita Duberry   | Executive Secretary    | 2019-03-13 | 53720.04  |
| 1005  | 1C       | Changhua         | Meg Holleran     | Executive Secretary    | 2014-10-20 | 73794.50  |


### Redundancy

`Deptlocation` is repeated for employees in the same department and can become inconsistent (example: `Deptcode=1C` appears with two locations).


## 2. Candidate key

Candidate key(s):
- `Empno` (assumed unique employee identifier).


## 3. Functional dependencies

Empno -> (Name, Job, Hiredate, Salary, Deptcode (in italics))

Deptcode -> (Deptlocation)

Transitive dependency:

Empno -> Deptcode -> Deptlocation

Note:
The sample data has an inconsistency for `Deptcode=1C` (`Pointe-a-Pitre` vs `Changhua`), therefore it can be treated as a data quality issue in the denormalized source, not as a valid business rule.

## 4. Step-by-step normalization

## Step A: 1NF

Overview:
All values are atomic, because there are not repeated groups, thus the table is already in 1NF.

Current relation:
Empno -> (Name, Job, Hiredate, Salary, Deptcode, Deptlocation)

There's Redundant department location data with  no data quality rules applied.

## Step B: 2NF

There's a Transitive dependency through `Deptcode`.

`Empno` is the primary key.


## Step C: 3NF

Decomposition:

EMPLOYEE (<u>Empno</u>, Name, Job, Hiredate, Salary, *Deptcode*)

DEPARTMENT (<u>Deptcode</u>, Deptlocation)

By diving it:
`Deptlocation` is stored once per department.
Employee rows keep only `Deptcode` as a reference.

## 5. Relationships

Empno -> (Name, Job, Hiredate, Salary, Deptcode (in italics))

Deptcode -> (Deptlocation)

## 6. Proposed SQL schema (3NF)

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
