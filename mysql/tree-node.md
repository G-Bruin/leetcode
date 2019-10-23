#### 中等

#### 描述

- 给一个 tree 表， id 是树节点的标识符，p_id 是父节点的标识符

- tree

|id    |p_id   |
| :---: | :----: | 
| 1  | null |
| 2  | 1    |
| 3  | 1    |
| 4  | 2    |
| 5  | 2    |

#### 每一种树的节点可以是这三种类型之一

- Leaf: 叶子节点
- Root: 根节点
- Inner: 内部节点

- 写一个查询打印节点id和节点的类型。由节点id排序输出。以上样本的结果

|id    |Type    |
| :---: | :----: | 
| 1  | Root |
| 2  | Inner|
| 3  | Leaf |
| 4  | Leaf |
| 5  | Leaf |


- 解析 

- id in (n, n+1,n+2)的记录里 people>=100
- id in (n, n-1,n+1)的记录里 people>=100
- id in (n, n-1,n-2)的记录里 people>=100


#### 解答

```shell script
SELECT
    atree.id,
    IF(ISNULL(atree.p_id),
        'Root',
        IF(atree.id IN (SELECT p_id FROM tree), 'Inner','Leaf')) Type
FROM
    tree atree
ORDER BY atree.id

```