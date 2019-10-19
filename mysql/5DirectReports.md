#### 中等难度

#### 描述

- Employee表保存所有员工包括他们的经理。每一位员工都有一个Id,和还有一个经理Id列

|Id    |Name 	  |Department |ManagerId |
| :---: | :----: | :----: | :----: | 
|101   |John 	  |A 	      |null      |
|102   |Dan 	  |A 	      |101       |
|103   |James 	  |A 	      |101       |
|104   |Amy 	  |A 	      |101       |
|105   |Anne 	  |A 	      |101       |
|106   |Ron 	  |B 	      |101       |

- 鉴于Employee表,编写一个SQL查询,查找至少有5名直接下属的经理

#### 解答
|Name|
| :---: |
|John|

```shell script
SELECT NAME 
FROM
	Employee 
HAVING
	( SELECT count( * ) FROM Employee AS p WHERE p.ManagerId = Employee.Id ) >= 5
```