---
title: 使用rinetd转发TCP连接
date: 2022-02-24 14:40:31
tags: Linux

---


公司内部由于安全限制，在本地无法直接连接线上数据库进行查询操作，需要通过内网开发机做转发。在工具选择上，团队采用了rinetd。

# rinetd简介
rinetd是一个支持TCP协议的端口转发工具，它是一个单进程服务，可以处理任意数量的地址端口对转发（通过在/etc/rinetd.conf中进行配置）

[![](使用rinetd转发/header.jpeg "官方网站")](http://www.rinetd.com/)

# 安装
##  1.编译安装
```shell
$ curl -LO 'http://www.rinetd.com/download/rinetd.tar.gz'
$ tar xvzf rinetd.tar.gz
$ cd rinetd
$ sed -i 's/65536/65535/g' rinetd.c # 修改端口范围，否则会报错
$ make
$ sudo make install
```
## 2.MacOS安装
```shell
$ brew install rinetd
```


## 3.Debian / Ubuntu

```shell
$ sudo apt update
$ sudo apt install rinetd
```

## 4.在 RHEL / CentOS 上借助 yum 安装

```shell
$ sudo vim /etc/yum.repos.d/nux-misc.repo

[nux-misc]
name=Nux Misc
baseurl=http://li.nux.ro/download/nux/misc/el6/x86_64/
enabled=0
gpgcheck=1
gpgkey=http://li.nux.ro/download/nux/RPM-GPG-KEY-nux.ro

sudo yum --enablerepo=nux-misc install rinetd
```


# 配置
配置文件路径为 /etc/rinetd.conf
```shell
#
# this is the configuration file for rinetd, the internet redirection server
#
# you may specify global allow and deny rules here
# only ip addresses are matched, hostnames cannot be specified here
# the wildcards you may use are * and ?
#
# allow 192.168.2.*
# deny 192.168.2.1?


#
# forwarding rules come here
#
# you may specify allow and deny rules after a specific forwarding rule
# to apply to only that forwarding rule
#
# bindadress    bindport  connectaddress  connectport
0.0.0.0 6379    r-ly25ac35fxxxxx.redis.rds.aliyuncs.com 6379


# logging information
logfile /var/log/rinetd.log

# uncomment the following line if you want web-server style logfile format
# logcommon
```

# 参考资料
<http://manpages.ubuntu.com/manpages/bionic/man8/rinetd.8.html>
<https://zhuanlan.zhihu.com/p/322487244>
<https://blog.csdn.net/u013755439/article/details/82079669>
<https://www.khow.me/blog/easily-forwarding-arbitrary-tcp-connections-with-rinetd.html>

