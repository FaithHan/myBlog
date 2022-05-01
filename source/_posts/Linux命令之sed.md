---
title: Linux命令之sed
date: 2022-04-24 15:53:48
tags:
---

# 什么是sed

sed是一个流式文本编辑器，可以执行搜索，查找替换，插入和删除操作，它的输入可以来自文件或这管道。



# 语法

```shell
sed [OPTION]... {script-only-if-no-other-script} [input-file]...  
```

# 用法

####  替换

如下将unix替换为linux

```shell
$sed 's/unix/linux/' geekfile.txt
```

# 参考

- [sed命令手册（非常有用）](https://www.gnu.org/software/sed/manual/sed.html#Execution-Cycle)

