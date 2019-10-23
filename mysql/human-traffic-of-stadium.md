#### 困难

#### 描述

- x 市新建了一个体育场，每天都会有访客并把数据记录到下列，id, visit_date, people
- 写一个查询来显示有3个或更多的连续的记录行和人的数量超过并包含100人数
- 结果集按照 Id 顺序， Month 倒序

- stadium

|Id    |visit_date  |people    |
| :---: | :----: | :----: | 
| 1    | 2017-01-01 | 10        |
| 2    | 2017-01-02 | 109       |
| 3    | 2017-01-03 | 150       |
| 4    | 2017-01-04 | 99        |
| 5    | 2017-01-05 | 145       |
| 6    | 2017-01-06 | 1455      |
| 7    | 2017-01-07 | 199       |
| 8    | 2017-01-08 | 188       |

- 输出

|Id    |visit_date  |people    |
| :---: | :----: | :----: | 
| 5    | 2017-01-05 | 145       |
| 6    | 2017-01-06 | 1455      |
| 7    | 2017-01-07 | 199       |
| 8    | 2017-01-08 | 188       |

- 解析 

- id in (n, n+1,n+2)的记录里 people>=100
- id in (n, n-1,n+1)的记录里 people>=100
- id in (n, n-1,n-2)的记录里 people>=100


#### 解答

```shell script
SELECT
	* 
FROM
	stadium a 
WHERE
	a.people >= 100 
	AND (
	(
	a.id + 1 IN ( SELECT id FROM stadium WHERE people >= 100 ) 
	AND a.id + 2 IN ( SELECT id FROM stadium WHERE people >= 100 ) 
	) 
	OR (
	a.id - 1 IN ( SELECT id FROM stadium WHERE people >= 100 ) 
	AND a.id + 1 IN ( SELECT id FROM stadium WHERE people >= 100 ) 
	) 
	OR (
	a.id - 1 IN ( SELECT id FROM stadium WHERE people >= 100 ) 
	AND a.id - 2 IN ( SELECT id FROM stadium WHERE people >= 100 ) 
	) 
	);
```