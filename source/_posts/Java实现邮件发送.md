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

### 依赖

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
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-mail</artifactId>
    <version>2.6.0</version>
</dependency>
```



### 使用Spring的JavaMailSender发送邮件

我们可以直接用jakarta mail提供的原生API发送邮件，但是Spring官方所提供的JavaMailSender有更为简洁和强大的接口

```java
// 实例化并配置JavaMailSender
JavaMailSenderImpl mailSender = new JavaMailSenderImpl();
mailSender.setHost("mail.baidu.com");
mailSender.setPort(25);
mailSender.setUsername("hanfei08");
mailSender.setPassword("******");

Properties props = mailSender.getJavaMailProperties();
props.put("mail.transport.protocol", "smtp");
props.put("mail.smtp.auth", "true");
props.put("mail.smtp.starttls.enable", "true");
props.put("mail.debug", "true");

/**
* 发送邮件
*/
public static void sendMail(String[] to, String[] cc, String[] bcc,
                             String subject, String content, PriorityEnum priority,
                             Map<String, InputStream> attachmentMap, Map<String, InputStream> inlineMap,
                             boolean isHTML) {
    Assert.notNull(to, "to array can not be null");
    Assert.notNull(subject, "subject can not be null");
    Assert.notNull(content, "content can not be null");
    try {
        MimeMessage message = SENDER.createMimeMessage();
        MimeMessageHelper helper = new MimeMessageHelper(message, true, StandardCharsets.UTF_8.name());
        helper.setFrom(from);
        helper.setTo(to);
        helper.setCc(cc != null ? cc : EMPTY_ARRAY);
        helper.setCc(bcc != null ? bcc : EMPTY_ARRAY);
        helper.setSubject(subject);
        helper.setText(content, isHTML);
        helper.setSentDate(new Date());
        helper.setEncodeFilenames(true); // 解决附件中文名称乱码
        priority = priority != null ? priority : NORMAL; //邮件重要程度
        switch (priority) {
            case LOW:
                helper.setPriority(5);
                break;
            case HIGH:
                helper.setPriority(1);
                break;
            case NORMAL:
            default:
        }
      //添加附件
        if (Objects.nonNull(attachmentMap)) {
            for (Map.Entry<String, InputStream> entry : attachmentMap.entrySet()) {
                String fileName = entry.getKey();
                InputStream inputStream = entry.getValue();
                helper.addAttachment(fileName, new ByteArrayResource(StreamCopyUtils.copyToByteArray(inputStream)));
            }
        }
      //添加资源
        if (isHTML && Objects.nonNull(inlineMap)) {
            for (Map.Entry<String, InputStream> entry : inlineMap.entrySet()) {
                String cuid = entry.getKey();
                InputStream inputStream = entry.getValue();
                helper.addInline(cuid, new ByteArrayResource(StreamCopyUtils.copyToByteArray(inputStream)){
                    @Override
                    public String getFilename() {
                        return cuid;
                    }
                });
            }
        }
        sendMessage(message);
    } catch (MessagingException | IOException e) {
        log.error("send mail error", e);
        throw new RuntimeException(e);
    }
}
```

# 参考

[https://www.javatpoint.com/java-mail-api-tutorial](https://www.javatpoint.com/java-mail-api-tutorial) 很好的教学包括发送各种类型的邮件、接收邮件、删除邮件等操作



