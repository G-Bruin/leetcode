#### 简单难度

#### 描述

- Person: PersonId 是上表主键

| 列名 | 类型 |
| :---: | :----: | 
| PersonId  | int | 
| FirstName | varchar |
| LastName  | varchar   | 

- Address: AddressId 是上表主键

| 列名 | 类型 |
| :---: | :----: | 
| AddressId | int | 
| PersonId  | int | 
| City      | varchar |
| State     | varchar   | 

- 编写一个 SQL 查询，满足条件：无论 person 是否有地址信息，都需要基于上述两表提供 person 的以下信息
```shell script
  FirstName, LastName, City, State
```

#### 解答

```shell script
select p.FirstName,p.LastName,a.City,a.State
from
person p left join address a
on
p.personid = a.personid
```