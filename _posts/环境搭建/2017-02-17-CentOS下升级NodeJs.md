---
layout : life
title : CentOS6.5下升级NodeJs
category : 环境搭建
duoshuo : true
date : 2017-02-17
---


******

	作者: daodaoliang
    版本: V 1.0.1
    邮箱：daodaoliang@yeah.net

<!-- more -->

  `NodeJs` 是什么就不在赘述，可一直接参考[英文官网][1]，或者[中文官网][2]，在项目中进行应用时，有时候需要用到最新版本的特性，但是CentOS系统为了稳定性，默认的源都是在该版本的操作系统发布时或者更新时的最稳定版本，所以仅仅是采用`yum update` 的操作是不能进行对应升级的。
  所以下面采用两种方式来进行在线升级。
  
### 0x01 用 `n` 模块来进行 `nodejs` 升级

  在 `NodeJs` 中有一个模块叫做 `n` 专门用来管理 `NodeJs` 的版本。
  
  * 首先下载安装模块 `n` 
  
  ```
    npm install -g n
  ```
  
  * 升级`NodeJs`到最新版本
  
  ```
    n stable
  ```
  
  * 升级`NodeJs`到指定版本
  
  ```
    n 0.10.23
  ```

### 0x02 用源码的方式进行编译安装

一般用方式一就可以完成升级安装，但是有时候会出现一些莫名其妙的错误，比如说是`segment fault`之类的错误，这个时候我只能用源码的方式进行编译安装。


  
  

[1]:https://nodejs.org/en/
[2]:http://nodejs.cn/