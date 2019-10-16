#### 简单难度

#### 描述

- 给定一个包含电话号码列表（一行一个电话号码）的文本文件 file.txt，写一个 bash 脚本输出所有有效的电话号码
- 你可以假设一个有效的电话号码必须满足以下两种格式： (xxx) xxx-xxxx 或 xxx-xxx-xxxx。（x 表示一个数字）
- 你也可以假设每行前后没有多余的空格字符
  
 #### 示例
 
 - 假设 file.txt 内容如下
 ```shell script
    987-123-4567
    123 456 7890
    (123) 456-7890
```
- 你的脚本应当输出下列有效的电话号码
```shell script
    987-123-4567
    (123) 456-7890
```

#### 解答

- grep 支持：BREs、EREs、PREs 正则表达式，[详情](https://blog.csdn.net/yufenghyc/article/details/51078107)

```shell script
cat file.txt | grep -P "(^\d{3}-|^\(\d{3}\) )\d{3}-\d{4}$"

cat file.txt | grep -E "(^[0-9]{3}-|^\([0-9]{3}\) )[0-9]{3}-[0-9]{4}$"
```