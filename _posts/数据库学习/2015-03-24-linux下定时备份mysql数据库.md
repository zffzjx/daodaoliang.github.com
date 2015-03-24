---
layout: life
title: linux下mysql定时备份
category: 数据库学习
duoshuo: true
date: 2015-03-34
---


<!-- more -->


### 1. 在服务器上建立备份文件的存放文件夹

```sh
	sudo mkdir /usr/local/dbbackup
```

### 2. 编写备份脚本

```sh
	vi dbbackup.sh 
```

在里面编写如下内容


### 3.更改备份脚本权限


```sh
	sudo chmod +x dbbackup.sh 
```


### 4.修改crontab定时执行脚本


```sh
	crontab -e 
```


#### 若每天晚上23点30备份，添加如下代码:


```sh
	30 23 * * * /usr/local/dbbackscripts/dbbackup.sh
```





