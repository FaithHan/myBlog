---
title: Linux命令之awk
date: 2022-04-23 17:43:55
tags:
---
# awk可以做什么
它一个脚本编程语言

**Linux命令之grep**
1. 按行扫描文件
2. 通过模式匹配每一行
3. 如果行匹配，则执行相应的action

[//]: # (![img.png]&#40;Linux命令之awk/img.png&#41;)
**用于**
1. 变换数据格式
2. 生成格式化报告

# 语法
```shell
awk 'BEGIN{ commands } pattern{ commands } END{ commands }'
```

# 内置变量
- NR (Number of Record)表示已经处理过的总记录数目,跨多个文件，
- NF (Number of Field)表示一条记录的字段的数目
- FS (Field Seperator)输入字段分隔符变量
```shell
$ awk -F 'FS' 'commands' inputfilename
或者
$ awk 'BEGIN{FS="FS";}'
```
- OFS(Output Field Separator)输出字段分隔符变量
- RS (Record Separator) 记录分隔符
- ORS (Output Record Separator) 输出记录分隔符变量
- FILENAME 当前输入文件的名字
- FNR 当前输入文件的记录数目
> NR和FNR可以结合使用，参考[https://www.runoob.com/w3cnote/8-awesome-awk-built-in-variables.html](https://www.runoob.com/w3cnote/8-awesome-awk-built-in-variables.html)

$1 $2 $3 表示第几个field（从1计数），$0表示整个行

# Pattern
- /regular expression/ 正则表达式，当行文本匹配时则执行Action
- expression 当返回非0或非null时，执行相应Action
- pat1, pat2 区间表达式
- BEGIN END 特殊的模式，在行匹配之前和匹配完成之后执行
- empty 空模式，匹配所有行


# Actions
- 一个action由一个或者多个awk语句组成，被大括号包围{}，语句之间通过换行符或分号进行分割
- 只要一条语句或者没有语句的action，也需要有大括号
- 如果完全省略Action（大括号也省略），则等同于'{print $0}'

```shell
/foo/  { }  # match foo, do nothing - empty action
/foo/       # match foo, print the record - omitted action
```

# 参考
- [工作原理](https://www.runoob.com/w3cnote/awk-work-principle.html)
- [入门教程](https://www.geeksforgeeks.org/awk-command-unixlinux-examples/)
- [官方手册](https://man7.org/linux/man-pages/man1/awk.1p.html)
- [AWK Patterns and Actions](https://www.math.utah.edu/docs/info/gawk_9.html#SEC97)
- [个人觉着不错的详细教程](https://www.grymoire.com/Unix/Awk.html#toc_You_can_buy_me_a_coffee.2C_please)








