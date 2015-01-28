---
layout : life
title: crtmpserver配置文件说明
category : 环境搭建
duoshuo: true
date : 2015-01-28
---

<!-- more -->

## ***配置文件说明***

配置文件实际上是一个Lua脚本，它包含至少一个configuration的对象，从而为程序提供灵活的扩展和定制功能。除了configuration对象外，还可以有函数，Lua库等。

### ***主结构***

```lua
configuration=
{
  daemon=false,
  pathSeparator="/",
  logAppenders=
  {
    -- content removed for clarity
  },
  applications=
  {
    -- content removed for clarity
  }
}
```

|key|type|mandatory|description|
|:------:|:------:|:-------:|:-------:|
|daemon|boolean|yes|true  表示 服务以后台方式启动;false 表示 服务以控制台模式启动(以用于开发);|
|pathSeparator|string(1)|yes|用来分隔路径; 例如，在UNIX-like是 /, Windows是\;|
|logAppenders|object|yes|配置日志追加的容器|
|applications|object|yes|配置加载各种应用的容器|

***服务启动时，将按顺序执行下列操作:***

* 配置文件加载后，首先做的就是对配置文件进行校验，如果配置文件有错误，将会有错误提示并停止启动，可进行修改后再启动;
* 读取 daemon 值，判断服务是以后台方式启动还是以控制台方式启动;
* 读取日志追加器，用来配置日志记录并启动到运行状态，依据日志追加器，可以看到更多的日志信息;
* 最后的应用加载，只到这一步完成后，服务和应用才在线，并准备就绪;

### ***日志追加器***

这部分包含了一个日志追加器的列表。整个日志追加器的添加是在加载时配置，依据日志级别，追加器可以选择是否有日志消息输出到指定目的处；

```lua
logAppenders=
{
  {
    name="console appender",
    type="coloredConsole",
    level=6
  },
  {
    name="file appender",
    type="file",
    level=6,
    fileName="/tmp/crtmpserver.log"
  }
},
```

|key|type|mandatory|description|
|:------:|:------:|:-------:|:-------:|
|name|string|yes|追加器的名字.|
|type|string|yes|追加器的类型
可以是控制台，带颜色控制台或文件；
控制台和带颜色控制台 都会将日志消息输出到控制台，
不同之处在于带颜色控制台会依据日志级别进行颜色标记；
文件类型则会将所有消息输出到指定的文件；|
|level|number|yes|日志的级别
可见下表中的级别定义；
只有小于或等于这个级别的日志消息会被记录，高于这个级别则都被丢弃；
例如:
  级别为0时，只记录 FATAL 消息；
  级别为3时，只记录 FATAL, ERROR, WARNING, INFO 消息；|
|fileName|string|yes|如果追加器类型为文件，则在此处指定日志文件和路径|
