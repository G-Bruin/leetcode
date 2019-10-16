#### 简单难度

#### 描述
- 编写一个 SQL 查询，查找 Person 表中所有重复的电子邮箱
- Employee 

| Id   | Email  |
| :---: | :----: |
| 1  | a@b.com |
| 2  | c@d.com |
| 3  | a@b.com |

- 根据以上输入，你的查询应返回以下结果：

| Email |
| :---: |
| a@b.com |

#### 解答

```shell script
SELECT email from Person GROUP BY email HAVING count(email) >1
```