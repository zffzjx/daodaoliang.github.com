---
layout : life
title : supervisor 安装与配置
category : 环境搭建
duoshuo : true
date : 2016-11-02
---


******
	作者: daodaoliang
    版本: V1.0.1
    邮箱： daodaoliang@yeah.net

[这里是官方链接][1]

<!-- more -->

## 0x00 supervisor 简介

Supervisor 是一个用 python 语言开发的用来在 linux 系统下进行进程管理的工具。可以很方面的监控、启动、停止、重启一个或者多个进程。当进程意外终止时可以在第一时间进行重启，做到自动恢复。

## 0x01 supervisor 安装

**1.确保 python 环境完备**

**Note:** Supervisor is known to work with Python 2.4 or later but will not work under any version of Python 3.

安装 [easy_install][2] 或者 [pip][3]：

```
	wget --no-check-certificate https://bootstrap.pypa.io/ez_setup.py -O - | sudo python
```

或者

```
	# get-pip.py请从官网获取
	python get-pip.py
```

安装 supervisor

```
	pip install supervisor
```

或者

```
	easy_install supervisor
```

或者

```
	# 需要源支持
	yum install supervisor
```

supervisor安装完成后会生成三个执行程序：supervisortd、supervisorctl、echo_supervisord_conf，分别是supervisor的守护进程服务（用于接收进程管理命令）、客户端（用于和守护进程通信，发送管理进程的指令）、生成初始配置文件程序。




[1]:http://supervisord.org/installing.html
[2]:https://pypi.python.org/pypi/setuptools
[3]:https://pip.pypa.io/en/stable/installing/

