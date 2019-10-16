#### 简单难度

#### 描述

- 给定一个文本文件 file.txt，请只打印这个文件中的第十行
  
 #### 示例
 
 - 假设 file.txt 内容如下
 ```shell script
     Line 1
     Line 2
     Line 3
     Line 4
     Line 5
     Line 6
     Line 7
     Line 8
     Line 9
     Line 10
```
- 应当输出
```shell script
    Line 10
```

#### 解答

```shell script
awk 'NR == 10' file.txt 
tail -n+10 file.txt|head -1 tail -n +10
```