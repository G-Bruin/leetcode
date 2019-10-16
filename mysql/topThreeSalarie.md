#### 困难

#### 描述
- Employee 表包含所有员工信息，每个员工有其对应的工号 Id，姓名 Name，工资 Salary 和部门编号 DepartmentId

| Id   | Name  | Salary  | DepartmentId  | 
| :---: | :----: | :----: | :----: | 
| 1  | Joe   | 85000  | 1            |
| 2  | Henry | 80000  | 2            |
| 3  | Sam   | 60000  | 2            |
| 4  | Max   | 90000  | 1            |
| 5  | Janet | 69000  | 1            |
| 6  | Randy | 85000  | 1            |
| 7  | Will  | 70000  | 1            |


- Department 表包含公司所有部门的信息

| Id  | Name |
| :---: |:---: |
| 1 | IT |
| 1 | Sales |

- 编写一个 SQL 查询，找出每个部门获得前三高工资的所有员工。例如，根据上述给定的表，查询结果应返回

| Department    | Employee  | Salary  | 
| :---: | :----: | :----: |
| IT         | Max      | 90000  |
| IT         | Randy    | 85000  |
| IT         | Joe      | 85000  |
| IT         | Will     | 70000  |
| Sales      | Henry    | 80000  |
| Sales      | Sam      | 60000  |

#### 解答

- 执行代码： 执行结果正确，提交却是错的，我暂时不知道错在哪儿里
```shell script
select t.salary as min_salary, t.Name as Department, Employee.Name as Employee, Employee.Salary from Employee , 
(

	SELECT *, IFNULL((

	SELECT DISTINCT(salary) from Employee, (select @i :=0, @pre := -1) t 
	where Employee.DepartmentId = Department.id 
	HAVING ( @i := @i + (@pre != (@pre := salary))) = 3 
	ORDER BY salary desc

	), 0) as salary from Department
	
) as t

where t.id = Employee.DepartmentId and Employee.Salary >= t.Salary
order by t.id asc, Employee.Salary desc;

```