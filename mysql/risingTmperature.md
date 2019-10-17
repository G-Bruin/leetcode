#### 简单 (个人觉得不简单)

#### 描述
- 给定一个 Weather 表，编写一个 SQL 查询，来查找与之前（昨天的）日期相比温度更高的所有日期的 Id

| Id(INT)   | RecordDate(DATE)  | Temperature(INT)    | 
| :---: | :----: | :----: 
|       1 |       2015-01-01 |               10 |
|       2 |       2015-01-02 |               25 |
|       3 |       2015-01-03 |               20 |
|       4 |       2015-01-04 |               30 |


- 例如，根据上述给定的 Weather 表格，返回如下 Id

| Id  |
| :---: 
|  2 |
|  4 |


#### 解答
- datediff 日期求差
- 执行代码
```shell script
select p.id from 

(select *, 
case 
	when @pre = null then 0
    when @pre < Temperature then 1 
    else 0 
end as type,

@pre := Temperature,

if(datediff(RecordDate,@date) = 1, 1, 0 ) as diff,

@date := RecordDate


from Weather, (select @pre := null, @date := null ) t ORDER BY RecordDate asc) p  
where p.type = 1 and p.diff = 1;

```