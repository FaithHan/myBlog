---
title: Java实现邮件发送
date: 2022-03-06 20:45:36
tags:
---

# 什么是SMTP、POP3和IMAP

首先我们需要对和邮件相关的三个协议有一个基本的认知

### SMTP

**SMTP** 的全称是“Simple Mail Transfer Protocol”，即简单邮件传输协议。它是一组用于从源地址到目的地址传输邮件的规范，通过它来控制邮件的中转方式。SMTP 协议属于 TCP/IP 协议簇，它帮助每台计算机在发送或中转信件时找到下一个目的地。SMTP 服务器就是遵循 SMTP 协议的发送邮件服务器。

### POP3

**POP3**是Post Office Protocol 3的简称，即邮局协议的第3个版本,它规定怎样将个人计算机连接到Internet的邮件服务器和下载电子邮件的电子协议。它是因特网电子邮件的第一个离线协议标准,POP3允许用户从服务器上把邮件存储到本地主机（即自己的计算机）上,同时删除保存在邮件服务器上的邮件，而POP3服务器则是遵循POP3协议的接收邮件服务器，用来接收电子邮件的

### IAMP

**IMAP**全称是Internet Mail Access Protocol，即交互式邮件存取协议，它是跟POP3类似邮件访问标准协议之一。不同的是，开启了IMAP后，您在电子邮件客户端收取的邮件仍然保留在服务器上，同时在客户端上的操作都会反馈到服务器上，如：删除邮件，标记已读等，服务器上的邮件也会做相应的动作。所以无论从浏览器登录邮箱或者客户端软件登录邮箱，看到的邮件以及状态都是一致的。

> 1. [Difference Between SMTP and POP3](https://techdifferences.com/difference-between-smtp-and-pop3.html)
> 2. [Difference Between POP3 and IMAP](https://techdifferences.com/difference-between-pop3-and-imap.html)
> 3. [一张图解释SMTP、POP和IMAP协议](https://blog.csdn.net/hyman_c/article/details/54612627)

# 使用Java发送邮件

需要引入的邮件发送Jar包

```xml
<!-- https://mvnrepository.com/artifact/com.sun.mail/jakarta.mail -->
<dependency>
    <groupId>com.sun.mail</groupId>
    <artifactId>jakarta.mail</artifactId>
    <version>2.0.1</version>
</dependency>

```

如果是SpringBoot项目，我们可以直接引入

```xml
```





