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

使用easy_install管理第三方库
============================

安装 `setuptools <https://pypi.python.org/pypi/setuptools>`_
-------------------------------------------------------------

可以直接下载压缩包，解压安装。或者对于联网的机器，也可以使用 `ez_setup.py <https://bootstrap.pypa.io/ez_setup.py>`_ 安装::

 python ez_setup.py
 
安装 `setuptools <https://pypi.python.org/pypi/setuptools>`_ 结束之后， easy_install也会被同时安装。
将easy_install的路径加入执行路径后，在console中就可以使用easy_install来安装python包，easy_install支持离线安装（zip包，tar包，exe包）和在线安装（PyPI URL），并且能自动下载安装依赖包::

 easy_install [options] package_pat/URL
 
.. note::

 对于使用代理的机器，在使用easy_install之前需要先设置console的环境变量来指明代理
 
 ``set http_proxy=...``
 
 ``set https_proxy=...``
 
使用pip管理第三方库（推荐）
============================

安装pip
-------------

pip已经在python 3.4中默认包含，如果使用的是其他的python版本，需要先安装pip，三种方法：

 1. 下载 `pip安装包 <https://pypi.python.org/pypi/pip/6.1.1>`_ 安装
 2. ``easy_install pip``
 3. 下载 `get-pip.py <https://raw.github.com/pypa/pip/master/contrib/get-pip.py>`_ ， 执行命令 ``python get-pip.py``
 
使用pip
--------

pip的用法和easy_install类似，但支持更多的功能::

    Usage:
      pip <command> [options]

    Commands:
      install                     Install packages.
      uninstall                   Uninstall packages.
      freeze                      Output installed packages in requirements format.
      list                        List installed packages.
      show                        Show information about installed packages.
      search                      Search PyPI for packages.
      wheel                       Build wheels from your requirements.
      zip                         DEPRECATED. Zip individual packages.
      unzip                       DEPRECATED. Unzip individual packages.
      help                        Show help for commands.

    General Options:
      -h, --help                  Show help.
      --isolated                  Run pip in an isolated mode, ignoring
                                  environment variables and user configuration.
      -v, --verbose               Give more output. Option is additive, and can be
                                  used up to 3 times.
      -V, --version               Show version and exit.
      -q, --quiet                 Give less output.
      --log <path>                Path to a verbose appending log.
      --proxy <proxy>             Specify a proxy in the form
                                  [user:passwd@]proxy.server:port.
      --retries <retries>         Maximum number of retries each connection should
                                  attempt (default 5 times).
      --timeout <sec>             Set the socket timeout (default 15 seconds).
      --exists-action <action>    Default action when a path already exists:
                                  (s)witch, (i)gnore, (w)ipe, (b)ackup.
      --trusted-host <hostname>   Mark this host as trusted, even though it does
                                  not have valid or any HTTPS.
      --cert <path>               Path to alternate CA bundle.
      --client-cert <path>        Path to SSL client certificate, a single file
                                  containing the private key and the certificate
                                  in PEM format.
      --cache-dir <dir>           Store the cache data in <dir>.
      --no-cache-dir              Disable the cache.
      --disable-pip-version-check
                                  Don't periodically check PyPI to determine
                                  whether a new version of pip is available for
                                  download. Implied with --no-index.

.. note::

 对于使用代理的机器，在使用pip时候需要指明代理
 
 pip install XXX --proxy <proxy> 
                                  
参考
=================

.. [1] https://docs.python.org/2/install/index.html
.. [2] https://python-packaging-user-guide.readthedocs.org/en/latest/index.html