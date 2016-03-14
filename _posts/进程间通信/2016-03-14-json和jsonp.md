---
layout : life
title : josn 和 jsonp (转载)
category : 进程间通信
duoshuo: true
date : 2016-03-14
---

******

原文在[这里](http://www.cnblogs.com/dowinning/archive/2012/04/19/json-jsonp-jquery.html), 为了自己温习方面，特地转载；

<!-- more -->


## 1. 前言：

说到AJAX就会不可避免的面临两个问题，第一个是AJAX以何种格式来交换数据？第二个是跨域的需求如何解决？这两个问题目前都有不同的解决方案，比如数据可以用自定义字符串或者用XML来描述，跨域可以通过服务器端代理来解决。

但到目前为止最被推崇或者说首选的方案还是用JSON来传数据，靠JSONP来跨域。而这就是本文将要讲述的内容。

JSON和JSONP虽然只有一个字母的差别，但其实他们根本不是一回事儿：JSON是一种数据交换格式，而JSONP是一种依靠开发人员的聪明才智创造出的一种非官方跨域数据交互协议。我们拿最近比较火的谍战片来打个比方，JSON是地下党们用来书写和交换情报的“暗号”，而JSONP则是把用暗号书写的情报传递给自己同志时使用的接头方式。看到没？一个是描述信息的格式，一个是信息传递双方约定的方法。

既然随便聊聊，那我们就不再采用教条的方式来讲述，而是把关注重心放在帮助开发人员理解是否应当选择使用以及如何使用上。

## 2.  什么是JSON？

前面简单说了一下，JSON是一种基于文本的数据交换方式，或者叫做数据描述格式，你是否该选用他首先肯定要关注它所拥有的优点。

### **2.1 JSON的优点：**

1. 基于纯文本，跨平台传递极其简单；
#. Javascript原生支持，后台语言几乎全部支持；
#. 轻量级数据格式，占用字符数量极少，特别适合互联网传递；
#. 可读性较强，虽然比不上XML那么一目了然，但在合理的依次缩进之后还是很容易识别的；
#. 容易编写和解析，当然前提是你要知道数据结构；

JSON的缺点当然也有，但在作者看来实在是无关紧要的东西，所以不再单独说明。

### **2.2 JSON的格式或者叫规则：**

JSON能够以非常简单的方式来描述数据结构，XML能做的它都能做，因此在跨平台方面两者完全不分伯仲。

1. JSON只有两种数据类型描述符，大括号{}和方括号[]，其余英文冒号:是映射符，英文逗号,是分隔符，英文双引号""是定义符。
#. 大括号{}用来描述一组“不同类型的无序键值对集合”（每个键值对可以理解为OOP的属性描述），方括号[]用来描述一组“相同类型的有序数据集合”（可对应OOP的数组）。
#. 上述两种集合中若有多个子项，则通过英文逗号,进行分隔。
#. 键值对以英文冒号:进行分隔，并且建议键名都加上英文双引号""，以便于不同语言的解析。
#. JSON内部常用数据类型无非就是字符串、数字、布尔、日期、null 这么几个，字符串必须用双引号引起来，其余的都不用，日期类型比较特殊，这里就不展开讲述了，只是建议如果客户端没有按日期排序功能需求的话，那么把日期时间直接作为字符串传递就好，可以省去很多麻烦。

### **JSON实例：**

```
	// 描述一个人
	
	var person = {
		"Name": "Bob",
		"Age": 32,
		"Company": "IBM",
		"Engineer": true
	}
	
	// 获取这个人的信息
	
	var personAge = person.Age;
	
	// 描述几个人
	
	var members = [
		{
			"Name": "Bob",
			"Age": 32,
			"Company": "IBM",
			"Engineer": true
		},
		{
			"Name": "John",
			"Age": 20,
			"Company": "Oracle",
			"Engineer": false
		},
		{
			"Name": "Henry",
			"Age": 45,
			"Company": "Microsoft",
			"Engineer": false
		}
	]
	
	// 读取其中John的公司名称
	
	var johnsCompany = members[1].Company;
	
	// 描述一次会议
	
	var conference = {
		"Conference": "Future Marketing",
		"Date": "2012-6-1",
		"Address": "Beijing",
		"Members": 
		[
			{
				"Name": "Bob",
				"Age": 32,
				"Company": "IBM",
				"Engineer": true
			},
			{
				"Name": "John",
				"Age": 20,
				"Company": "Oracle",
				"Engineer": false
			},
			{
				"Name": "Henry",
				"Age": 45,
				"Company": "Microsoft",
				"Engineer": false
			}
		]
	}
	
	// 读取参会者Henry是否工程师
	
	var henryIsAnEngineer = conference.Members[2].Engineer;
```