#### 困难

#### 描述
- EEmployee表保存所有员工。employee表有三列:员工id、公司名称、和工资

| Id   | Company  | Salary   | 
| :---: | :----: | :----: |
|1    | A          | 2341   |
|2    | A          | 341    |
|3    | A          | 15     |
|4    | A          | 15314  |
|5    | A          | 451    |
|6    | A          | 513    |
|7    | B          | 15     |
|8    | B          | 13     |
|9    | B          | 1154   |
|10   | B          | 1345   |
|11   | B          | 1221   |
|12   | B          | 234    |
|13   | C          | 2345   |
|14   | C          | 2645   |
|15   | C          | 2645   |
|16   | C          | 2652   |
|17   | C          | 65     |


- 编写一个SQL查询来找到每个公司的工资中位数。如果你能解决它不使用任何内置的SQL函数加分

| Id   | Company  | Salary   | 
| :---: | :----: | :----: |
|5    | A          | 451    |
|6    | A          | 513    |
|12   | B          | 234    |
|9    | B          | 1154   |
|14   | C          | 2645   |


#### 解答

```shell script

SELECT Id, Company, Salary from (
SELECT
	id,
	Company,
	Salary,
	if(@company = Company, @rank := @rank + 1, @rank := 1 )	as rank,
	@company := Company,
	
	(select count(*) from Employee as p1  where  p1.Company = Employee.Company) as total
	
FROM
	Employee,
	( SELECT @company := null, @rank := 1 ) AS t 
ORDER BY
	Employee.Company,
	Employee.Salary 
	
	)
	as p2 where p2.rank = FLOOR((total + 1) / 2)  or p2.rank = FLOOR((total + 2) / 2)
```