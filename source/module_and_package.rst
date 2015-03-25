.. _`python module and package`:

=========================
python module and package
=========================

:Page Status: Development
:Last Reviewed: 

1 模块
=======

模块是一个包含各种定义和数据的python文件，在模块中模块名存储于全局变量 ``__name__`` 中

1.1 加载模块
------------------

可以通过 ``import module`` 和 ``from module import item`` 加载模块和模块中的全局成员。
模块中的代码会在被加载时执行。

.. note::
 
 对于同一个进程，多次import只会加载一次模块，需要重新加载模块，需要用 ``reload`` 函数
 
.. note::
 
 需要根据模块名动态加载模块，可以使用 ``__import__`` 函数

1.2 直接执行模块
------------------

被其他模块加载时，模块的 ``__name__`` 变量值是模块的名字。
当直接用python执行模块的时候 ``__name__`` 变量值变成 ``__main__`` ，
可以通过检查此变量的名字来确定此文件是否被直接执行

::

 if __name__ == "__main__":
     print("Being executed directly")

1.3 使用 ``dir()`` 和 ``help()`` 查看模块中的成员和帮助信息
----------------------------------------------------

想知道一个模块中有哪些成员，可以直接查看代码或者相应的代码。或者我们可以打开一个python解析器，使用 ``dir`` 函数

::

 >>>import(os)
 >>>dir(os.path)
 ['__all__', '__builtins__', '__doc__', '__file__', '__name__', '__package__', '_
 abspath_split', '_getfullpathname', 'abspath', 'altsep', 'basename', 'commonpref
 ix', 'curdir', 'defpath', 'devnull', 'dirname', 'exists', 'expanduser', 'expandv
 ars', 'extsep', 'genericpath', 'getatime', 'getctime', 'getmtime', 'getsize', 'i
 sabs', 'isdir', 'isfile', 'islink', 'ismount', 'join', 'lexists', 'normcase', 'n
 ormpath', 'os', 'pardir', 'pathsep', 'realpath', 'relpath', 'sep', 'split', 'spl
 itdrive', 'splitext', 'splitunc', 'stat', 'supports_unicode_filenames', 'sys', '
 walk', 'warnings']

想知道某个模块成员的用法，使用 ``help`` 函数。当然前提是此模块成员提供了相应的document。

::

 >>> help(os.path.join)
 Help on function join in module ntpath:

 join(path, *paths)
     Join two or more pathname components, inserting "\" as needed.

1.4 __builtin__模块
--------------------

在python解析器中，__builtin__模块中的成员可以直接使用，不需要在之前加载__builtin__模块。


__builtin__模块中的成员的具体信息可以参见 `python标准文档2~6章 <https://docs.python.org/2/library/index.html>`_

2. 包
=======

python包形式上就是一个含有 ``__init__.py`` 文件和其他模块的文件夹，python包可以用来结构化的组织python模块。

2.1 加载包
---------------

可以通过 ``import package.subpackage...module`` 或 ``from package.subpackage import module`` 的形式来访问包中的模块。

.. note::

 第一层的包需要在 ``sys.path`` 中：
 
 - 脚本所在的目录
 - 环境变量 PYTHONPATH
 - 默认的python lib路径

2.2 相对路径加载包
------------------

.. note::

 不推荐使用相对路径加载包
 
包中模块可以通过相对路径来访问包中的其他模块

3. 第三方包管理
========================

python的一大优点是第三方包/库的丰富易用

我们将在 ``packaging_and_sharing`` 一章中介绍python库的结构，在这边我们先介绍如果获取和管理第三方库

3.1 PyPI （别名： 奶酪商店）
------------------------














* Download package source, run command "python setup.py install"
* Use easy_install tool
* Use pip tool
