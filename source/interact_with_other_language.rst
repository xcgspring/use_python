.. _`interact_with_other_language`:

=========================
python与其他语言交互
=========================

:Page Status: Development
:Last Reviewed: 

python的一大特性就是能和很多语言方便的交互，所以python经常被称为胶水语言。

使用 ``ctypes`` 访问第三方C动态库 [1]_ [2]_
===========================================

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

使用 ``comtypes`` 访问COM组件 [7]_
==========================================

windows平台上大部分模块基于COM技术，对COM的支持使得python能支持大部分的windows上的模块

在没有comtypes的情况下，利用ole.dll中的C函数也可以实现对COM组件的访问 [8]_ ，但需要自己处理COM组件和python之间的数据结构的差异，编程效率低

下面是comtypes中访问COM组件的代码节选::

 #COM functions are in ole32.dll
 from ctypes import oledll
 _ole32 = oledll.ole32
 _ole32_nohresult = windll.ole32
 
 #init COM
 _ole32.CoInitializeEx(None, None)
 
 #create COM object instance
 _ole32.CoCreateInstance(byref(clsid), punkouter, clsctx, byref(iid), byref(p))
 
 #use COM functions
 p.func1()
 p.func2()
 
 #deinit COM
 _ole32_nohresult.CoUninitialize()
 
.. note::

 COM组件使用regsvr32.exe注册时，将COM组件的信息（dll的信息，clsid，progid）写入注册表，需要使用时再根据clsid或progid从注册表中查找dll的信息 [9]_
 
 既可以直接使用regedit来查看注册的COM组件信息，也可以用专门的工具oleview.exe （in WDK）来查看

利用comtypes，可以用纯python代码实现对所有类型COM组件的访问（custom类型的，支持dispatch接口类型的），并且支持编写COM组件

.. note::

 ``pywin32`` 不支持对custom类型的COM组件的访问

通过clsid，progid，来访问COM组件
---------------------------------

如果我们知道了COM组件的clsid或progid，可以通过comtypes.client中的CreateObject函数来访问COM组件::

 instance = CreateObject(clsid/progid)

通过typelib，dll文件来访问COM组件
---------------------------------

如果我们不知道COM组件的clsid或progid，但知道dll文件的路径，我们可以使用oleview.exe来查看clsid，或者可以通过comtypes.client中的GetModule函数来生成python binding，然后从python binding中查找clsid和iid::

 module = GetModule(typelib/dll/exe)
 dir(module)

构建自己的c/c++扩展
===============================

一个最简单的c扩展，来自python源代码PC/example_nt/example.c::

    #include "Python.h"

    static PyObject *
    ex_foo(PyObject *self, PyObject *args)
    {
        printf("Hello, world\n");
        Py_INCREF(Py_None);
        return Py_None;
    }

    static PyMethodDef example_methods[] = {
        {"foo", ex_foo, METH_VARARGS, "foo() doc string"},
        {NULL, NULL}
    };

    PyMODINIT_FUNC
    initexample(void)
    {
        Py_InitModule("example", example_methods);
    }

在python中调用此模块的代码如下::

    >>> import example
    >>> example
    <module 'example' from 'example.pyd'>
    >>> example.foo()
    Hello, world
    >>> help(example.foo)
    Help on built-in function foo in module example:

    foo(...)
        foo() doc string

    
从中可以看出，一个基本的c扩展包含以下部分：

1. 最开始 ``#include "Python.h"``
2. 模块方法实现
3. 模块接口定义
4. 模块初始化函数

更多内容见 `Extending Python with C or C++` [4]_ 

.. note::

 需要实现更复杂的c扩展，可以利用python源代码中Modules/xxmodule.c作为模板
 
.. note::

 c++扩展中会被python调用的方法，应该用 ``extern "C"`` 声明
 
 可以使用 `Boost.Python <http://www.boost.org/doc/libs/1_57_0/libs/python/doc/>`_ 库来简化c++扩展

用 ``distutils`` 编译c/c++扩展
-------------------------------

当完成c/c++扩展的编写，为了能让python能够顺利访问扩展中的成员，我们还需要将c/c++源码编译成动态库.so/.pyd [3]_

同样看一个简单的sample，来自python源代码PC/example_nt/setup.py::

    from distutils.core import setup, Extension

    example_mod = Extension('example', sources = ['example.c'])

    setup(name = "example",
        version = "1.0",
        description = "A sample extension module",
        ext_modules = [example_mod],
    )

扩展的编译是通过distutils中的Extension类来完成的，详见 [10]_

.. note::

 如果在windows上编译遇到 ``error: Unable to find vcvarsall.bat``
 
 则需要设置环境变量，将 ``VS90COMNTOOLS`` 设置为VS的Tools路径

 比如， 如果你安装的是2013版 ``SET VS90COMNTOOLS=%VS120COMNTOOLS%``

向c/c++程序里面内嵌python代码
===============================

示例代码::

    #include <Python.h>

    int
    main(int argc, char *argv[])
    {
      Py_SetProgramName(argv[0]);  /* optional but recommended */
      Py_Initialize();
      PyRun_SimpleString("from time import time,ctime\n"
                         "print 'Today is',ctime(time())\n");
      Py_Finalize();
      return 0;
    }

简单内嵌步奏：

1. 将程序名传入python解析器，使用函数Py_SetProgramName()
2. 初始化python解析器，使用函数Py_Initialize()
3. 执行python代码或文件，使用函数PyRun_SimpleString(),PyRun_SimpleFile()
4. 关闭python解析器


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
.. [9] https://msdn.microsoft.com/en-us/library/windows/desktop/ms683954(v=vs.85).aspx
.. [10] https://docs.python.org/2/distutils/apiref.html#distutils.core.Distribution
