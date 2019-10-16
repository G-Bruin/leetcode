#### 中等难度

#### 描述
- 编写一个 SQL 查询，查找所有至少连续出现三次的数字

- Logs 

| Id   | Num  | 
| :---: | :----: | 
| 1  |  1  |
| 2  |  1  |
| 3  |  1  |
| 4  |  2  |
| 5  |  1  |
| 6  |  2  |
| 7  |  2  |


- 例如，给定上面的 Logs 表， 1 是唯一连续出现至少三次的数字

| ConsecutiveNums    |  
| :---: | 
| 1 |


#### 解答

```shell script
select distinct Num as ConsecutiveNums
from (
  select Num, 
    case 
      when @prev = Num then @count := @count + 1
      when (@prev := Num) then @count := 1
    end as count
  from logs, (select @prev := -1, @count := 0) as t
) as temp
where temp.count >= 3

```