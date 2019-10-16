#### 简单难度

#### 描述
- 某网站包含两个表，Customers 表和 Orders 表。编写一个 SQL 查询，找出所有从不订购任何东西的客户
- Customers  

| Id   | Name  |
| :---: | :----: |
| 1  | Joe   |
| 2  | Henry |
| 3  | Sam   |
| 4  | Max   |

- Orders

| Id   | CustomerId  |
| :---: | :----: |
| 1  | 3          |
| 2  | 1          |

- 例如给定上述表格，你的查询应返回：

| Customers  |
| :---: |
| Henry     |
| Max       |

#### 解答

```shell script
SELECT name as Customers  from Customers where id not in (SELECT CustomerId from Orders )
```