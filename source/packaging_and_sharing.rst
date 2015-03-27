.. _`packaging_and_sharing`:

=========================
打包并发布
=========================

:Page Status: Development
:Last Reviewed: 

之前的一章我们介绍了如何下载和管理第三方库，这里我们介绍如何生成并发布我们自己的库

python库结构
====================

一般的python库结构::

    package folder -+
                    |
                    +setup.py        <--主要的配置/安装文件，必须
                    |
                    +setup.cfg       <--提供给用户的配置文件，可选
                    |
                    +README          <--readme文件，可选
                    |
                    +MANIFEST.in     <--打包配置文件模板，用来和setup.py一起生成打包配置文件MANIFEST，可选
                    |
                    +<your package>  <--你的package，最好与package folder名字一致
                    |
                    +<other files>   <--额外的文件

利用 ``distutils`` 打包
========================

``disutils`` 是python的标准库，提供了基本的工具集来打包和发布python库， 同时也确立了python库的基本结构。

我们可以利用 ``disutils`` 来快速的为我们自己的package构建一个标准的库，步奏如下::

    1. 创建package同名文件夹
    2. 将package放到文件夹中，同时新建文件setup.py
    3. 编辑setup.py文件，从disutils.core中加载setup函数，并给setup函数添加参数（project信息）
    4. 如果需要，添加MANIFEST.in，来处理setup.py打包时没有添加库里面的文件，见 `MANIFEST.in语法 <https://docs.python.org/3.4/distutils/sourcedist.html#specifying-the-files-to-distribute>`_
    5. 运行命令python setup.py sdist生成库

setup函数的参数::

    name
    工程名字，名字中可以包含的字符见 `PEP426 <http://legacy.python.org/dev/peps/pep-0426/#name>`_

    version
    工程版本，格式见 `PEP440 <https://pypa.io/en/latest/peps/#pep440s>`_:
    
        1.2.0.dev1  # Development release
        1.2.0a1     # Alpha Release
        1.2.0b1     # Beta Release
        1.2.0rc1    # RC Release
        1.2.0       # Final Release
        1.2.0.post1 # Post Release

    description        
    工程描述

    url              
    工程地址

    author           
    作者信息

    license         
    许可证信息

    classifiers
    一组你的工程相关的信息，PyPI会利用这些信息来给你的工程分类，见 https://pypi.python.org/pypi?%3Aaction=list_classifiers

    keywords
    一组关键字来描述你的工程

    packages         
    你的工程中包含的package，需要列出所需的所有package和subpackage，disutils不会自动寻找subpackage

    install_requires
    依赖列表，pip安装时候会根据这个列表来自动安装所需依赖库，比如sphinx的依赖列表::
    
        install_requires = [
        'six>=1.4',
        'Jinja2>=2.3',
        'Pygments>=1.2',
        'docutils>=0.10',
        'snowballstemmer>=1.1',
        'babel',
        ]

    package_data
    package中的数据列表，生成库的时候这个列表中的数据都会被加进MANIFEST文件
    安装库的时候，这个列表中的数据会被安装

    data_files
    和package_data的区别在于，data_files列出的数据不在package中

    scripts
    entry_points
    console_scripts

.. note::

    如果使用python2.6或之前的版本，即使package_data中列出了文件，在MANIFEST.in仍然需要再添加一遍

利用 ``setuptools`` 打包 （推荐）
=============================

``setuptools`` 是另一款第三方的打包发布工具集，兼容 ``disutils`` 的库结构

``setuptools`` 的使用步骤和 ``disutils`` 类似，添加优化了一些功能，使得打包发布更加容易

主要增强的功能有：

- 自动查找/下载/安装/升级库的依赖
- 自动包含所有的packages，不需要全部列出了
- 自动包含所有的相关的data文件，不需要新建一个MANIFEST.in文件了

新增或改变的setup函数的参数::

    include_package_data
    设成True，则自动添加你的工程目录中的所有的文件，如果没有额外的指明，只添加全部的文件

    exclude_package_data
    指明了需要排除的文件

    package_data
    指明了需要添加的文件

    zip_safe
    指明你的工程是否能够以压缩的格式安装

    install_requires
    依赖

.. note::

    其他的关键字见 `setuptools新增改变的关键字列表 <http://pythonhosted.org/setuptools/setuptools.html#basic-use>`_

.. note::

    setuptools 通过find_packages函数来自动包含所有的packages，对于大型软件来说，极大的方便了packages的管理

    ::
    
        find(cls, where='.', exclude=(), include=('*',)) 

        method of __builtin__.type instance
        Return a list all Python packages found within directory 'where'

        'where' should be supplied as a "cross-platform" (i.e. URL-style)
        path; it will be converted to the appropriate local path syntax.
        'exclude' is a sequence of package names to exclude; '*' can be used
        as a wildcard in the names, such that 'foo.*' will exclude all
        subpackages of 'foo' (but not 'foo' itself).

        'include' is a sequence of package names to include.  If it's
        specified, only the named packages will be included.  If it's not
        specified, all found packages will be included.  'include' can contain
        shell style wildcard patterns just like 'exclude'.

        The list of included packages is built up first and then any
        explicitly excluded packages are removed from it.

.. note::

    对于使用setuptools来打包的库，用户安装使用之前需要安装合适版本的setuptools

    setuptools为本机没有安装setuptools的用户提供了一个解决方法，在安装库之前自动安装setuptools：

    下载 `ez_setup.py <https://bootstrap.pypa.io/ez_setup.py>`_ ，并包含在库根文件夹下

    同时在setup.py中添加::

        try:
            from setuptools import setup, find_packages
        except ImportError:
            import ez_setup
            ez_setup.use_setuptools()
            from setuptools import setup, find_packages

上传库到PyPI
=================

1. 注册账号，建议通过 `PyPI用户注册界面 <https://pypi.python.org/pypi?%3Aaction=register_form>`_ 完成注册
2. 注册工程，建议通过 `PyPI工程注册界面 <https://pypi.python.org/pypi?%3Aaction=submit_form>`_ 完成注册
3. 上传工程，建议使用 `twine <https://python-packaging-user-guide.readthedocs.org/en/latest/projects.html#twine>`_ 来上传

::

 twine upload dist/*

.. note::

 PyPI不推荐使用 ``python setup.py register`` 来完成用户注册和工程注册，因为这种方式会使用明文来传输你的用户名和密码
 
 同样的原因， 也不推荐使用 ``python setup.py sdist upload`` 来上传工程
 


参考
=================

.. [1] https://docs.python.org/2/distutils/index.html
.. [2] http://pythonhosted.org/setuptools/setuptools.html
.. [3] https://python-packaging-user-guide.readthedocs.org/en/latest/distributing.html
.. [4] https://python-packaging-user-guide.readthedocs.org/en/latest/current.html
