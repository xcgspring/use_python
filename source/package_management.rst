.. _`package_management`:

=========================
python包管理
=========================

:Page Status: Development
:Last Reviewed: 

python的一大优点是第三方库的丰富易用

我们将在 :ref:`packaging_and_sharing` 一章中介绍python库的结构，在这边我们先介绍如果获取和管理第三方库

PyPI （别名： 奶酪商店）
========================

PyPI是python官方的第三方库的仓库，所有人都可以下载第三方库或上传自己开发的库到PyPI

PyPI推荐使用pip包管理器来下载第三方库。

手工下载安装库
=====================

直接下载并解压库的zip或者tar.gz包，运行命令 ``python setup.py install``

.. note::

 如果提示找不到setuptools，需要先安装setuptools库
 
.. note::

 这种安装方法不会自动安装库的依赖


使用pip管理第三方库（推荐）
============================

安装pip
-------------

pip已经在python 3.4中默认包含，如果使用的是其他的python版本，需要先安装pip

 - 下载 `get-pip.py <https://raw.github.com/pypa/pip/master/contrib/get-pip.py>`_

 - 执行命令 ``python get-pip.py``

.. note::

 如果工作机使用代理上网，需要设置环境变量来指明代理服务器后， 才能执行命令 ``python get-pip.py``
 
使用pip下载安装第三方库
-------------------------

安装最新版本的库:

::

 pip install 'SomeProject'


安装特定版本的库:

::

 pip install 'SomeProject==1.4'

使用pip升级第三方库
------------------------

将已有的库升级到最新版本：

::

 pip install --upgrade SomeProject


参考
=================

.. [1] https://docs.python.org/2/install/index.html
.. [2] https://python-packaging-user-guide.readthedocs.org/en/latest/index.html