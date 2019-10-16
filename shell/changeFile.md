#### 中等难度

#### 描述

- 给定一个文件 file.txt，转置它的内容
- 你可以假设每行列数相同，并且每个字段由 ' ' 分隔
  
 #### 示例
 
 - 假设 file.txt 内容如下
 ```shell script
    name age
    alice 21
    ryan 30
```
- 应当输出
```shell script
    name alice ryan
    age 21 30
```

#### 解答

- NF代表的是一个文本文件中一行（一条记录）中的字段个数 
- NR代表的是这个文本文件的行数（记录数）
- 循环拼接 NF=1 || NF=2 的值，并输出res
```shell script
 awk '{ for (i=1; i<=NF; i++) { if(NR==1) {res[i]=$i;} else { res[i]=res[i] " " $i; } } } END { for (i=1; i<=NF; i++) { print res[i] } } ' file.txt
```