Leecode database: [URL](https://leetcode.com/problemset/database/)

Start: 15/11/2020

End:

### Interesting....
`You can't specify target table 'person' for update in FROM clause`

-- you can't modify the same table which you use in the SELECT part.

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

### 182. Duplicate Emails
```
select Email from Person
group by Email
having count(*) > 1

select t1.email from (
    select email , count(*) as cnt from person
    group by email
    having cnt > 1
)t1
```

### 183. Customers Who Never Order
```
select name as customers from
(
    select c.name, o.customerid from customers c 
    left join orders o on c.id = o.CustomerId
)t1
where customerid is null

select c.name as Customers from customers c 
left join orders o on c.id = o.CustomerId
where o.customerid is null

SELECT A.Name as Customers from Customers A
LEFT JOIN Orders B on  a.Id = B.CustomerId
WHERE b.CustomerId is NULL

SELECT A.Name from Customers A
WHERE A.Id NOT IN (SELECT B.CustomerId from Orders B)
```

### 184. Department Highest Salary
```
select department,Employee,Salary
from(
    select 
    d.name as Department, e.name as Employee, e.salary as Salary, 
    DENSE_RANK() OVER(PARTITION BY e.departmentid ORDER BY e.salary desc) as "rank"
    from employee e left join department d
    on e.departmentid = d.id
)t1
where t1.rank = 1 and t1.Department is not null
```

### 185. Department Top Three Salaries
```
select department,Employee,Salary
from(
    select 
    d.name as Department, e.name as Employee, e.salary as Salary, 
    DENSE_RANK() OVER(PARTITION BY e.departmentid ORDER BY e.salary desc) as "rank"
    from employee e left join department d
    on e.departmentid = d.id
)t1
where t1.rank <= 3 and t1.Department is not null


SELECT
    d.Name AS 'Department', e1.Name AS 'Employee', e1.Salary
FROM
    Employee e1
        JOIN
    Department d ON e1.DepartmentId = d.Id
WHERE
    3 > (SELECT
            COUNT(DISTINCT e2.Salary)
        FROM
            Employee e2
        WHERE
            e2.Salary > e1.Salary
                AND e1.DepartmentId = e2.DepartmentId
        )
;
```
### 196. Delete Duplicate Emails
```
delete P1
from Person p1, Person P2
where p1.email = p2.email 
and p1.id > p2.id
```

### 197. Rising Temperature
```
SELECT t1.Id FROM weather t1, weather t2
WHERE subdate(t1.recordDate, 1) = t2.recordDate  AND t1.Temperature > t2.Temperature

subdate: https://www.w3schools.com/sql/func_mysql_subdate.asp
```

### 262. Trips and Users***
```
select t.Request_at Day,
       ROUND((count(IF(t.status!='completed',TRUE,null))/count(*)),2) as 'Cancellation Rate'
from Trips t where 
t.Client_Id in (Select Users_Id from Users where Banned='No') 
and t.Driver_Id in (Select Users_Id from Users where Banned='No')
and t.Request_at between '2013-10-01' and '2013-10-03'
group by t.Request_at;
```

###
```
```

###
```
```

###
```
```

