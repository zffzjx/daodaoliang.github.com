---
layout : life
title : 日常linux命令之iftop
category : linux学习
duoshuo : true
date : 2016-05-23
---


******

	作者: daodaoliang
    时间: 2016年5月23日
    版本: v0.0.1
    邮箱: daodaoliang@yeah.net

<!-- more -->

日常用的网络流量查看工具为 `iftop`， 但是他仅仅只能简单的查看网络的流量情况，若是想要查看某个链接的流量情况就比较困难了，因此再次推荐`iftop` 这个工具

### 0x01 安装 iftop

[我是官方网站](http://www.ex-parrot.com/pdw/iftop/)

**编译安装iftop示例:**

```
    # centos
    yum install flex byacc  libpcap ncurses ncurses-devel libpcap-devel

    # debian
    apt-get install flex byacc  libpcap0.8 libncurses5
```

```
    wget http://www.ex-parrot.com/pdw/iftop/download/iftop-0.17.tar.gz

    tar zxvf iftop-0.17.tar.gz

    cd iftop-0.17

    ./configure

    make && make install
```

**一键安装iftop 示例:**

```
    # 安装EPEL源

    # CentOS/RHEL 5 ：
    rpm -Uvh https://dl.fedoraproject.org/pub/epel/epel-release-latest-5.noarch.rpm

    # CentOS/RHEL 6 ：
    rpm -Uvh https://dl.fedoraproject.org/pub/epel/epel-release-latest-6.noarch.rpm

    # CentOS/RHEL 7 ：
    rpm -Uvh https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
```

```
    # centos
    yum install iftop

    # debian
    apt-get install iftop
```

### 0x02 使用 iftop

直接执行

```
    iftop -i eth1
```

![iftop](/res/img/blog/linux学习/iftop.png)


