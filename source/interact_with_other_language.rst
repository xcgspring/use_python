.. _`interact_with_other_language`:

=========================
python与其他语言交互
=========================

:Page Status: Development
:Last Reviewed: 

python的一大特性就是能和很多语言方便的交互，所以python经常被称为胶水语言。

使用 ``ctypes`` 访问第三方C动态库
===============================

Windows平台
-------------

在32bit的Windows系统上，对 ``__cdecl`` 和 ``__stdcall`` 声明的函数，编译时函数名会使用不同的命名规则 [6]_

比如编译如下C代码::

    int _cdecl    f (int x) { return 0; }
    int _stdcall  g (int y) { return 0; }
    int _fastcall h (int z) { return 0; }

32bit的编译器会输出::

    _f
    _g@4
    @h@4

cdll使用 ``__cdecl`` 声明函数， windll和oledll使用 ``__stdcall`` 声明函数

oledll比一般的windll额外指定了返回值的类型，为 ``HRESULT``，见 `OleDLL <https://docs.python.org/2/library/ctypes.html#ctypes.OleDLL>`_

所以ctypes为windows系统提供了三种dll的类来区分使用，windows上既可以通过属性来访问dll，也可以通过 ``cdll.LoadLibrary`` 来访问::

    >>> from ctypes import *
    >>> print windll.kernel32 
    <WinDLL 'kernel32', handle ... at ...>
    >>> print cdll.msvcrt 
    <CDLL 'msvcrt', handle ... at ...>
    >>> libc = cdll.msvcrt 
    >>>


Linux平台
-------------

linux平台上仅有cdll，linux平台上需要指明动态库的全名，通过 ``cdll.LoadLibrary`` 来访问::

    >>> cdll.LoadLibrary("libc.so.6") 
    <CDLL 'libc.so.6', handle ... at ...>
    >>> libc = CDLL("libc.so.6")     
    >>> libc                         
    <CDLL 'libc.so.6', handle ... at ...>
    >>>

.. note::

 ctypes不能支持加载c++的动态库 [5]_

使用 ``comtypes`` 访问COM组件
===============================

windows平台上大部分模块基于COM技术，对COM的支持使得python能支持大部分的windows上的模块

在没有comtypes的情况下，利用ole.dll中的C函数也可以实现对COM组件的访问 [8]_ ，但编程效率太低了

用comtypes可以用纯python代码实现对COM组件的访问（custom类型的，支持dispatch接口类型的），并且支持编写COM组件

.. note::

 ``pywin32`` 不支持对custom类型的COM组件的访问






构建自己的c/c++扩展
===============================


向c/c++程序里面内嵌python代码
===============================


参考
=================

.. [1] http://starship.python.net/crew/theller/ctypes/
.. [2] https://docs.python.org/2/library/ctypes.html
.. [3] https://docs.python.org/2/faq/windows.html#is-a-pyd-file-the-same-as-a-dll
.. [4] https://docs.python.org/2/extending/index.html
.. [5] http://blog.vrplumber.com/b/2007/07/21/ctypes-for-c-is/
.. [6] http://en.wikipedia.org/wiki/Name_mangling#C_name_decoration_in_Microsoft_Windows
.. [7] https://pythonhosted.org/comtypes/
.. [8] http://www.codeproject.com/Articles/13601/COM-in-plain-C#C
