---
layout : life
title:  reStructuredText 的基本语法
category : 项目工程管理
duoshuo: true
date : 2015-12-22
---

reStructuredText [官方网址](http://docutils.sourceforge.net/rst.html), 打不开吧!!!!!! fuck [GFW](https://zh.wikipedia.org/wiki/%E9%98%B2%E7%81%AB%E9%95%BF%E5%9F%8E)

<!-- more -->

[这里](http://sphinx-doc-zh.readthedocs.org/en/latest/rest.html)是Sphinx中关于`reStructuredText`的翻译，本文也是从里面挑拣自己平时回经常用到的语法进行示例化记录。

```

.. note::

    我是note 信息

.. attention::

    我是attention信息

.. caution::

    我是caution信息

.. warning::

    我是warning信息

.. tip::

    我是tip信息

.. important::

    我是important信息

.. hint::

    我是hint信息

.. error::

    我是error信息

.. danger::

    我是danger信息

============
文章标题测试
============

***************
章节标题测试
***************

小节标题测试
===============

子节标题测试
------------------

子子节标题测试
^^^^^^^^^^^^^^^^^^^^^

段落标题测试
""""""""""""""""""

段落标题测试
******************

**加黑字体**

*意大利斜体*

``I am code``

我是代码测试快::

    # coding: utf-8

    __author__ = 'daodaoliang'

    from flask import Flask
    from flask_restful import Resource, Api

    app = Flask(__name__)
    api = Api(app)


    # noinspection PyMethodMayBeStatic
    class Api_HelloWorld_V1(Resource):
        def get(self):
            return {'hello': 'world'}


    api.add_resource(Api_HelloWorld_V1, '/')

    if __name__ == '__main__':
        app.run(debug=True)

接下来时一个表格
---------------------

+------------------------+------------+----------+----------+
| Header row, column 1   | Header 2   | Header 3 | Header 4 |
| (header rows optional) |            |          |          |
+========================+============+==========+==========+
| body row 1, column 1   | column 2   | column 3 | column 4 |
+------------------------+------------+----------+----------+
| body row 2             | ...        | ...      |          |
+------------------------+------------+----------+----------+

`我的博客啦 <http://daodaoliang.github.io>`_.

`我的博客啦啦啦啦`_.

.. _我的博客啦啦啦啦: http://daodaoliang.github.io

.. image::
    https://pic4.zhimg.com/6a97b4a68a4db3f1d3ae66cd1638965f.jpeg

.. 这里是注释
```

![这里示例图01](/res/img/blog/项目工程管理/2015-12-22-01.png)

![这里示例图02](/res/img/blog/项目工程管理/2015-12-22-02.png)

![这里示例图03](/res/img/blog/项目工程管理/2015-12-22-03.png)




