.. _`用sphinx组织文档`:

================================
用sphinx组织文档
================================

:Page Status: Development
:Last Reviewed: 

sphinx是一个文本builder，能将一组reStructureText文档转换成其他格式（HTML， LaTex），能自动解析处理reStructureText标记。

安装sphinx
============

建议通过easy_install或pip来安装sphinx，能够自动处理依赖，简单迅速。

使用sphinx
============

sphinx提供了工具来简化了文档工程的配置和生成，使得用户能够更加专注于文档的内容。

对于一般的文档工程，使用sphinx通常包含有几个步奏， 见 `sphinx初尝 <http://sphinx-doc-zh.readthedocs.org/en/latest/tutorial.html>`_

1. 使用工具sphinx-quickstart快速配置文档资源
2. 修改index.rst来定义文档结构
3. 使用reStructureText添加文档内容
4. build，输出结果

sphinx的更多内容
=================

上面4个步奏已经可以满足大部分一般用户的需求，如果用户需要使用sphinx的更多功能（更多标记，更多扩展，定制模板），则需要对sphinx有更多的了解。

sphinx域
---------------

sphinx域是为某些语言输出提供特定的语法， 内置的支持包含python，c，c++，javascript，reStructureText。见 `sphinx domain <http://sphinx-doc-zh.readthedocs.org/en/latest/domains.html>`_

比如我想输出一个python的函数

想要得到的效果::

 format_exception(etype, value, tb[, limit=None])
  Format the exception with a traceback.

  Parameters: •etype – exception type
              •value – exception value
              •tb – traceback object
              •limit (integer or None) – maximum number of stack frames to show
             
  Return type: list of strings
 
在文档中的写法:: 

 .. py:function:: format_exception(etype, value, tb[, limit=None])

   Format the exception with a traceback.

   :param etype: exception type
   :param value: exception value
   :param tb: traceback object
   :param limit: maximum number of stack frames to show
   :type limit: integer or None
   :rtype: list of strings


配置sphinx
------------

见 `The build configuration file <http://sphinx-doc-zh.readthedocs.org/en/latest/config.html>`_

模板
------------

sphinx使用 `Jinja <http://jinja.pocoo.org/>`_ 作为HTML的模板语言

扩展
------------



Autodoc
^^^^^^^^^^^^


sphinx的一些技巧
=================