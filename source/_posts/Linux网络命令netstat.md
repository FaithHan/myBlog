---
title: Linux网络命令netstat
date: 2022-05-01 22:30:22
tags:
---
# Mac查看端口占用方法：
* -a - 查询所有端口，包含服务进程用到的端口
* -n - 显示IP，不展示名称，可以加快命令执行速度
* -v - 详细输出，如PID
* -p - 协议过滤，如 TCP UDP

```shell
#查询占用80短裤的进程
netstat -anvp TCP | egrep -w [.]80.*LISTEN
```

# Linux查看端口的方法
* -a - 查询所有端口，包含服务进程用到的端口
* -t - 查看TCP协议端口
* -u - 查看UDP协议端口
* -l - 查看处于listen状态的端口
* -p - 显示进程
