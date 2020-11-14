### 175. Combine Two Tables
```
select person.firstname, person.lastname, address.city, address.state 
from person left join address 
on person.personid = address.personid;
```

### 176. Second Highest Salary
```
SELECT max(Salary) as SecondHighestSalary
FROM Employee
WHERE Salary < (SELECT max(Salary) FROM Employee) 
```

177. Nth Highest Salary
```
CREATE FUNCTION getNthHighestSalary(N INT) RETURNS INT
BEGIN
DECLARE M INT;
SET M=N-1; #
  RETURN (
      # Write your MySQL query statement below.
      SELECT DISTINCT Salary FROM Employee ORDER BY Salary DESC LIMIT M, 1
  );
END

# LIMIT offset, count;
# The `offset` specifies the offset of the first row to return. The offset of the first row is 0, not 1.
# The `count` specifies maximum number of rows to return.
```
