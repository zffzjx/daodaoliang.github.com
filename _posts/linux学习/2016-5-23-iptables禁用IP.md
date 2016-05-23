---
layout : life
title: iptables禁用IP
category : linux学习
duoshuo: true
date : 2016-5-23
---


    作者: daodaoliang
    时间: 2016-5-23
    版本: V0.0.1
    邮箱: daodaoliang@yeah.net

<!-- more -->

******

### 0x01 确保服务启动

```
    service iptables status
    /etc/init.d/iptables stop
    /etc/init.d/iptables start
```

### 0x02 禁用IP

**禁用单个IP:**

```
    iptables -I INPUT -s 114.113.112.111 -j DROP
```

**禁用IP段的命令:**

```
    iptables -I INPUT -s 114.113.0.0/16 -j DROP
    iptables -I INPUT -s 114.112.0.0/16 -j DROP
    iptables -I INPUT -s 114.111.1.0/24 -j DROP
    iptables -I INPUT -s 114.111.2.0/24 -j DROP
```

**禁用整个IP段的命令:**

```
    iptables -I INPUT -s 114.0.0.0/8 -j DROP
```

### 0x03 服务器自启动






