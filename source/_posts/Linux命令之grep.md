---
title: Linux命令之grep
date: 2022-04-23 17:07:22
tags: Shell
---
# 什么是grep
grep能够在给定文件中，搜索包含与给定的模式匹配的行，对于开发人员和系统管理员来说，它是 Linux 和类 Unix 系统上最有用的命令之一。

# 基本语法

```shell
grep [OPTION...] PATTERNS [FILE...] # 基本正则表达式
grep [OPTION...] -e PATTERNS ... [FILE...] # 扩展正则表达式
grep [OPTION...] -f PATTERN_FILE ... [FILE...] #匹配字符串
```
**PS**
>  Basic vs Extended Regular Expressions In basic regular expressions the meta-characters ?, +, {, |, (, and )
> lose their special meaning; instead use the backslashed versions \\?, \\+, \\{, \\|, \\(, and \\).
# grep选项解释

### Pattern Syntax

-E 扩展正则表达式
-F 匹配字符串
-G 默认选项，基本正则表达式
-P Perl兼容正则表达式

### Matching Control
-e 可以接多个正则，如果匹配其中一个，则该行匹配
-i 忽略大小写
-v 选择不匹配的行（条件反转）
-w 只选择匹配整个单词的行
-x 只选中匹配整个行的

### General Output Control
-c 输出匹配行的数量
--color 将匹配的单词进行标记
-l 输出含有匹配行的文件（-L相反）
-o 只输出匹配项

###  Output Line Prefix Control
-H 包括文件名，默认
-h 不包括文件名

### Context Line Control
-A NUM 输出匹配行后面NUM行
-B NUM 输出匹配行前面NUM行
-C NUM 输出匹配行前后NUM行


# 参考文档

[官方手册](https://man7.org/linux/man-pages/man1/grep.1.html)
[Regular Expressions in Grep](https://linuxize.com/post/regular-expressions-in-grep)






