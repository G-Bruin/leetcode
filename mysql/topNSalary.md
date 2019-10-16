#### 中等难度

#### 描述
- 编写一个 SQL 查询，获取 Employee 表中第n高的薪水（Salary）
- Employee 

| Id   | Salary  | 
| :---: | :----: | 
| 1  | 100 |
| 2  | 200 | 
| 3  | 300 | 

- 上述 Employee 表，n = 2 时, SQL查询应该返回 200 。如果不存在第n高的薪水，那么查询应返回 null

| SecondHighestSalary  |
| :---: |
| 200                  |

#### 解答

```shell script
CREATE FUNCTION getNthHighestSalary(N INT) RETURNS INT
BEGIN
  SET N = N-1;
  IF N < 0 THEN
  RETURN NULL;
  ELSE
  RETURN (
      # Write your MySQL query statement below.
      SELECT IFNULL(
          (
          SELECT
          DISTINCT Salary
          FROM Employee
          ORDER BY Salary DESC
          LIMIT N, 1
          ), NULL)
      AS getNthHighestSalary
  );
  END IF;
END
```