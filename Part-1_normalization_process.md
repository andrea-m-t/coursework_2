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
The sample data has an inconsistency for `Deptcode=1C` (`Pointe-a-Pitre` vs `Changhua`), therefore it will be treated as a data quality issue in the denormalized source, not as a valid business rule.

## 4. Step-by-step normalization

## Step A: 1NF

Overview:
All values are atomic, because there are not repeated groups, therefore the table is already in 1NF.

Current relation:
R (<u>Empno</u>, Deptcode, Deptlocation, Name, Job, Hiredate, Salary)

Redundant department location data.

## Step B: 2NF

Condition:
- No partial dependency of non-key attributes on part of a composite key.

Analysis:
- The key is a single attribute (`Empno`), so partial dependencies cannot exist.

Result:
- The relation remains unchanged and is in 2NF.

Current relation:
R (<u>Empno</u>, Deptcode, Deptlocation, Name, Job, Hiredate, Salary)

Problem still present:
- Transitive dependency through `Deptcode`.

## Step C: 3NF

Condition:
- No transitive dependency from key to non-key attributes through another non-key attribute.

Violation found:
- `Empno -> Deptcode` and `Deptcode -> Deptlocation`

Decomposition:

EMPLOYEE (<u>Empno</u>, Name, Job, Hiredate, Salary, *Deptcode*)

DEPARTMENT (<u>Deptcode</u>, Deptlocation)

Why this fixes it:
- `Deptlocation` is stored once per department.
- Employee rows keep only `Deptcode` as a reference.
- Update, insert, and delete anomalies for department location are removed.

## 5. Relationships

DEPARTMENT (<u>Deptcode</u>, Deptlocation)

EMPLOYEE (<u>Empno</u>, Name, Job, Hiredate, Salary, *Deptcode*)

*Deptcode* references DEPARTMENT(<u>Deptcode</u>)

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
