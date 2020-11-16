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

### 177. Nth Highest Salary
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

### 178. Rank Scores
```
select score, DENSE_RANK() OVER(ORDER BY score desc) as "rank" from Scores;
```

### 180. Consecutive Numbers (3)
```
select distinct Num as ConsecutiveNums
from Logs
where (id+1, Num) in (select * from Logs) and (Id + 2, Num) in (select * from Logs)


SELECT DISTINCT
    l1.Num AS ConsecutiveNums
FROM
    Logs l1,
    Logs l2,
    Logs l3
WHERE
    l1.Id = l2.Id - 1
    AND l2.Id = l3.Id - 1
    AND l1.Num = l2.Num
    AND l2.Num = l3.Num
;
```

### 181. Employees Earning More Than Their Managers
```
select t1.employee from (
    select e.name as employee, m.name,  e.salary as s1, m.salary as s2
    from employee e join employee m
    on e.managerid = m.id
)t1
where s1 > s2;
```
