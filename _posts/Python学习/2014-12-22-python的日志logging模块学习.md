---
layout : life
title: python 的日志logging模块学习
category : Python学习
duoshuo: true
date : 2014-12-22
---

<!-- more -->

* **1.简单的将日志打印到屏幕**

```python
import logging

logging.debug('This is debug message')
logging.info('This is info message')
logging.warning('This is warning message')
```

屏幕上打印:

> WARNING:root:This is warning message

默认情况下，logging将日志打印到屏幕，日志级别为WARNING；
日志级别大小关系为：CRITICAL > ERROR > WARNING > INFO > DEBUG > NOTSET，当然也可以自己定义日志级别。


