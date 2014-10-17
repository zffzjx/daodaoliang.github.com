---
layout: post
title: Java学习日志之Servlet
category: java
date: 2014-09-17
---
## Java学习日志之Servlet

###**Part1.什么是Servlet?**
- 顾名思义Servlet就是服务器小程序，这个服务器可以是HTTP服务，也可以是邮件服务，也可以是FTP服务等等
- java Web 应用中的请求-相应都是交给Servlet来完成
- 原理图如下: 
<img src="http://www.blogjava.net/images/blogjava_net/fancydeepin/myself/servlet.png" width="200px" height="200px" align="right"/>

###**Part2.Servelt相关接口**
    **HttpServlet**类已经实现了Servlet接口所有方法，写Servlet时只需要继承这个类就行。

- **doGet**与**doPost**:   
 - 这俩对应的就是HTTP报文中的GET与POST方法，也是最常用的两个。   
 - Get通常用于请求服务器发送某个资源。   
 - Post通常用来向服务器输入数据，通常用来支持HTML表单。   
 其他HTTP方法工作原理可参见**“HTTP权威指南”**      
    对应的包与类：
{% highlight java %}
    javax.servlet.http.HttpServlet   
    Class HttpServlet   
{% endhighlight %}   

- **request**与**response**
{% highlight java %}
    1. 客户端发出的请求被封装成一个叫HTTPServletRequest类的对象，request对象包含了基本的请求信息。
    2. request常用方法：见api文档接口HTTPServletRequest中.
{% endhighlight %}
    3.服务器的响应封装到了HttpServletResponse类的对象，想对客户端下手就用response的方法～～
    4.response常用方法：见api文档接口HttpServeltResponse.

- **关于Web.xml的相关**
   1. <servlet>标签用于配置，部署servlet
   {% highlight java %}
        <servlet-name>Servlet name </servlet-name>//随意取名，但必须唯一
        <servlet-class>package.servletclass </servlet-class>//servlet类名
        <servlet-mapping>//设置访问方式
            <servlet-name>Servlet name</servlet-name>//与上面的对应
            <url-pattern>/XXX/FirstServlet </url-pattern>//访问路径
            <url-pattern>/XXX/FirstServlet.asp</url-pattern>//这里可以映射多个路径，以掩饰用啥玩意开发的
        </servlet-mapping>
        以上两个必须有，部署servlet所用
        <init-param>//初始化参数
            <param-name>message </param-name>//参数名称
            <param-value>value </param-value>//参数值
        </init-param>
   {% endhighlight %}

未完。。。。
