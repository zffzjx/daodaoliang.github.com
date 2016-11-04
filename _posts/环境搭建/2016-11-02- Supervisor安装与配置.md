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

**2.安装 supervisor**

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

## 0x02 supervisor 配置

**1. 配置文件生成**

运行supervisord服务的时候，需要用 c 参数指定supervisor配置文件，如果没有显示指定，默认以此在以下目录查找：

+ `$CWD/supervisord.conf`
+ `$CWD/etc/supervisord.conf`
+ `/etc/supervisord.conf`
+ `/etc/supervisor/supervisord.conf (since Supervisor 3.3.0)`
+ `../etc/supervisord.conf (Relative to the executable)`
+ `../supervisord.conf (Relative to the executable)`

**Note：** `$CWD` 表示运行 `supervisord` 程序的目录。

可以通过运行 `echo_supervisord_conf` 程序生成 `supervisor` 的初始化配置文件,如下所示:

```
	mkdir /etc/supervisor
    echo_supervisord_conf > /etc/supervisor/supervisord.conf
```

**2. 配置项说明**

supervisor的配置参数较多，下面介绍一下常用的参数配置，详细的配置及说明，请参考[官方文档][4]介绍。分号（;）开头的配置表示注释

```ini

[unix_http_server]

;socket文件的路径，supervisorctl用XML_RPC和supervisord通信就是通过它进行的,不设置的话，默认为none。非必须设置。
file=/tmp/supervisor.sock

;修改file的权限必须为0700,非必须设置。
chmod=0700

;修改file的权限的所属组为nobody:nogroup,非必需设置。
chown=nobody:nogroup

;使用supervisorctl链接的时候,认证的用户,不设置的话默认不需要用户,非必需设置。
username=user

;和上面的用户名对应的密码，可以直接使用明码，也可以使用SHA加密如{SHA}82ab876d1387bfafe46cc1c8a2ef074eae50cb1d。
password=123

;侦听在TCP上的socket,Web Server和远程的supervisorctl都要用到他不设置的话，默认为不开启。非必须设置。
[inet_http_server]

;侦听的IP和端口，侦听所有IP用 :9001或*:9001或者0.0.0.0:9001.这个必须设置，只要上面的[inet_http_server]开启了，就必须设置它。
port=127.0.0.1:9001

;登录时的用户名。
username=user

;登录时的密码。
password=123

;定义supervisord这个服务端进程的一些参数的。
[supervisord]

;supervisord这个主进程的日志路径,默认路径$CWD/supervisord.log,$CWD是当前目录,非必需设置。
logfile=/tmp/supervisord.log

;这个是上面那个日志文件的最大的大小,当超过50M(默认值是50M)的时候,会生成一个新的日志文件。当设置为0时,表示不限制文件大小,非必须设置。
logfile_maxbytes=50MB

;日志文件保持的数量,supervisor在启动程序时,会自动创建10个buckup文件(默认10),用于log rotate当设置为0时,表示不限制文件的数量。
logfile_backups=10

;日志级别，有critical, error, warn, info, debug, trace, or blather等默认为info,非必须设置项。
loglevel=info

;supervisord的pid文件路径,默认为$CWD/supervisord.pid。
pidfile=/tmp/supervisord.pid

;如果是true,supervisord进程将在前台运行默认为false,也就是后台以守护进程运行。
nodaemon=false

;这个是最少系统空闲的文件描述符，低于这个值(默认值1024)supervisor将不会启动。系统的文件描述符在这里设置cat /proc/sys/fs/file-max。
minfds=1024

;最小可用的进程描述符,低于这个值(默认200)supervisor也将不会正常启动。ulimit  -u这个命令，可以查看linux下面用户的最大进程数。
minprocs=200

;进程创建文件的掩码,默认为022
umask=022

;这个参数可以设置一个非root用户，当我们以root用户启动supervisord之后。我这里面设置的这个用户，也可以对supervisord进行管理,默认不设置。
user=daodaoliang

;supervisord的标识符，主要是给XML_RPC用的。当你有多个supervisor的时候，而且想调用XML_RPC统一管理，就需要为每个supervisor设置不同的标识符了,默认sipervisor。
identifier=supervisor

;当supervisord作为守护进程运行的时候,设置这个参数的话,启动supervisord进程之前,会先切换到这个目录默认不设置。
directory=/tmp

;在supervisord进程启动的时候，把以前子进程产生的日志文件(路径为AUTO的情况下)清除掉,默认false,有调试需求的同学可以设置为true。
nocleanup=true

;当子进程日志路径为AUTO的时候，子进程日志文件的存放路径。默认路径是这个东西，执行下面的这个命令看看就OK了，处理的东西就默认路径
;python -c "import tempfile;print tempfile.gettempdir()"
childlogdir=/tmp

;设置环境变量的，supervisord在linux中启动默认继承了linux的环境变量，在这里可以设置supervisord进程特有的其他环境变量。
;supervisord启动子进程时，子进程会拷贝父进程的内存空间内容。 所以设置的这些环境变量也会被子进程继承。
;小例子：environment=name="daodaoliang",age="26"
environment=KEY="value"

;如果设置为true，会清除子进程日志中的所有 ANSI 序列（\n,\t等）。
strip_ansi=false

[rpcinterface:supervisor]

supervisor.rpcinterface_factory = supervisor.rpcinterface:make_main_rpcinterface

;针对supervisorctl的一些配置
[supervisorctl]

;supervisorctl本地连接supervisord的时候，本地UNIX socket路径，注意这个是和前面的[unix_http_server]对应的默认值就是unix:///tmp/supervisor.sock
serverurl=unix:///tmp/supervisor.sock

;supervisorctl远程连接supervisord的时候，用到的TCP socket路径,注意这个和前面的[inet_http_server]对应默认就是http://127.0.0.1:9001
serverurl=http://127.0.0.1:9001

;用户名
username=daodaoliang

;密码
password=123

;输入用户名密码时候的提示符
prompt=iamnami

;这个参数和shell中的history类似，我们可以用上下键来查找前面执行过的命令默认是no file,所以我们想要有这种功能，必须指定一个文件
history_file=~/.sc_history

;要管理的子进程了,":"后面的是名字，最好别乱写和实际进程有点关联最好。这样的program我们可以设置一个或多个，一个program就是要被管理的一个进程
[program:theprogramname]


```



[1]:http://supervisord.org/installing.html
[2]:https://pypi.python.org/pypi/setuptools
[3]:https://pip.pypa.io/en/stable/installing/
[4]:http://supervisord.org/configuration.html

