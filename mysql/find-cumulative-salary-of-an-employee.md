#### 困难

#### 描述

- Employee 保存着薪资信息
- 编写SQL查询员工三个月内的薪资累计金额, 但排除最近的月份
- 结果集按照 Id 顺序， Month 倒序

|Id    |Month  	  |Salary  |
| :---: | :----: | :----: | 
| 1  | 1     | 20     |
| 2  | 1     | 20     |
| 1  | 2     | 30     |
| 2  | 2     | 30     |
| 3  | 2     | 40     |
| 1  | 3     | 40     |
| 3  | 3     | 60     |
| 1  | 4     | 60     |
| 3  | 4     | 70     |

- 输出

|Id    |Month  	  |Salary  |
| :---: | :----: | :----: | 
| 1  | 3     | 90     |
| 1  | 2     | 50     |
| 1  | 1     | 20     |
| 2  | 1     | 20     |
| 3  | 3     | 100    |
| 3  | 2     | 40     |

- 解析 

- 比如查找 id 是 1 的数据的结果
- 排除最近的 4月份， 1月份工资20， 2月份工资30， 3月份工资40，那每个月的累加金额是 

|Id    |Month  	  |Salary  |
| :---: | :----: | :----: | 
| 1  | 3     | 90     |
| 1  | 2     | 50     |
| 1  | 1     | 20     |

#### 解答

```shell script
select Id, Month, score as Salary  from 
(
    SELECT
        *,
        case 
        when @id = 0 then @score := Salary
        when @id = id then @score := @score + Salary
        else  @score := Salary 
        end as score,
        if(@id = id, @row := @row +1, @row := 1) as row,
        @id := id
        
    FROM
        Employee AS p, (select @score := 0, @id := 0, @row := 1) as t
    HAVING
        ( SELECT max( Month ) FROM Employee WHERE Employee.Id = p.Id ) > Month 
        
    ORDER BY
        id ASC,
        Month ASC
)
 as p1 where row <= 3 order by id ASC, Month desc
```