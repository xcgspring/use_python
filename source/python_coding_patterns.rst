.. _`python coding patterns`:

=========================
python编程模式
=========================

本章介绍python编程中常用到的一些模式，面向有一定python编程经验的程序员，来提高和完善自己的python知识。

初学者最好首先参考一本python入门读本，推荐O'REILLY出版的 **learning python**

logging模块的使用
=======================

logging模块的使用能大大增强程序的可调试性，建议所有的python应用和库都使用logging来输出信息。

参见 `python guide -- logging <http://docs.python-guide.org/en/latest/writing/logging/>`_

everything is object
=======================

Python是一门动态语言，所有的类型（函数，类，实例）都是一个object，可以被赋值给任意的变量，给python编程带来非常大的灵活性。

代码示例，动态调用函数::

    functions = {
        "func1": func1,
        "func2": func2,
    }

    def func1():
        print(1)
        
    def func2():
        print(2)
        
    if __name__=="__main__":
        import sys
        func_name = sys.argv[1]
        functions[func_name]()
    
迭代器和组合操作
=======================

迭代器
-------------------

迭代器可以有多种实现方式：

* 实现__iter__和next方法的object， 参见 `iterator-types <https://docs.python.org/2/library/stdtypes.html#iterator-types>`_
* 使用yield的generator， 参见 `yield expressions <https://docs.python.org/2/reference/expressions.html#yieldexpr>`_
* 使用built-in函数iter构造的迭代器， 参见 `iter statement <https://docs.python.org/2/library/functions.html#iter>`_

迭代器的使用：

* 用在for表达式中， 参见 `for statement <https://docs.python.org/2/reference/compound_stmts.html#for>`_

组合操作
--------------------

组合操作比一般的循环操作节省代码，而且能提高性能，python推荐使用组合操作来替代一般的循环操作。

组合操作形式::

 [ [expression] for object in iter_object [for_or_if_expression] ]

示例1::

    >>> res = []
    >>> for line in open('script1.py'):
    ... if line[0] == 'p':
    ... res.append(line.rstrip())
    ...
    >>> res
    ['print(sys.path)', 'print(2 ** 33)']
    
::

    >>> lines = [line.rstrip() for line in open('script1.py') if line[0] == 'p']
    >>> lines
    ['print(sys.path)', 'print(2 ** 33)']

示例2::

    >>> res = []
    >>> for x in 'abc':
    ... for y in 'lmn':
    ... res.append(x + y)
    ...
    >>> res
    ['al', 'am', 'an', 'bl', 'bm', 'bn', 'cl', 'cm', 'cn']

::
    
    >>> [x + y for x in 'abc' for y in 'lmn']
    ['al', 'am', 'an', 'bl', 'bm', 'bn', 'cl', 'cm', 'cn']

动态加载模块
=======================

Python通过 `__import__ <https://docs.python.org/2/library/functions.html#__import__>`_ 函数支持动态加载模块

动态加载os模块::

 os_module = __import__("os")

动态加载os.path模块::

 os_path_module = __import__("os.path", fromlist=["join"])
 
.. note::

 如果没有fromlist参数，即使模块名字是 ``os.path``，也只会返回os模块::
 
  os_module = __import__("os.path")
  
.. note::

 在python 2.7和python 3之后，也可以使用 `importlib.import_module() <https://docs.python.org/2/library/importlib.html#importlib.import_module>`_ 来动态加载模块

return VS exception
=======================

关于使用返回值还是使用异常的建议：
    
1. 我们应该对使用返回值的情景和使用异常的情景进行区分，使用返回值来表达函数的状态是不推荐的，会导致上层编码风格的混乱
2. 只使用返回值来传递数据，如果函数没有想要返回的值，尽量不要在函数中使用return，python会默认返回None
3. 使用具体的异常类型，比如built-in的 ``ValueError``, ``AttributeError``， 不要使用 ``Exception``， 如果需要自定义异常，将自定义的异常统一放到一个模块中，这样上层代码能方便访问你的自定义异常
4. 尽量统一在上层处理异常，中间层尽量不处理异常，让异常扩散到统一处理异常的地方

property VS method
=======================

关于使用属性还是方法的建议：

1. 属性一般意味着从内存中直接拿出之前存储的值
2. 方法意味着需要一定的处理
3. 如果设计上想让外部以为是属性，但需要一定的内部处理，可以使用 `@property <https://docs.python.org/2/library/functions.html#property>`_ 修饰

Unicode
=======================

线程和全局锁(GIL)
=======================

`GIL <https://docs.python.org/2/glossary.html#term-global-interpreter-lock>`_ 使得python的解析器运行在一个单线程上，简化python的解析器的实现，提高性能。
代价是python中多线程不能把load分配给CPU的多核， 参见 `Thread State and the Global Interpreter Lock <https://docs.python.org/2/c-api/init.html?highlight=gil#thread-state-and-the-global-interpreter-lock>`_

所以在python执行并行任务，可以尽量使用多进程来提高效率 `multiprocessing <https://docs.python.org/2/library/multiprocessing.html>`_

当然，在必须使用线程的情况下，比如UI应用，可以使用python提供的线程库 `threading <https://docs.python.org/2/library/threading.html>`_，但是不能利用CPU的多核来提高性能。

垃圾回收机制
=======================

Python有一个自动的垃圾回收机制，原理如下：

* python解析器对所有的object做引用计数，每次垃圾回收时，没有被引用的object会被free
* 当内存分配的object足够多的时候，python垃圾回收会自动运行，自动垃圾回收的频率可以通过 ``gc.set_threshold`` 设置
* python垃圾回收机制将object分成三类， threshold0~threshold2， object的threshold越高， 执行自动垃圾回收的频率越低
* python垃圾回收会释放循环引用的object
* 循环引用，且包含__del__方法的object，不会被垃圾回收释放
* 可以通过调用 ``gc.collect`` 手动运行垃圾回收

.. note::

 频繁的垃圾回收对python应用的性能有明显影响，所以运行垃圾回收需要有一些注意：
 
 * 不要频繁的运行垃圾回收
 * 在不经常运行的代码后面加入手动垃圾回收
 * 在性能要求高的代码段不要运行垃圾回收，在这些代码段运行接收再进行垃圾回收
 
更多参考：

* `Python_Garbage_Collection <http://www.digi.com/wiki/developer/index.php/Python_Garbage_Collection>`_
* `Python垃圾回收(gc)拖累了程序执行性能？ <http://blog.csdn.net/overstack/article/details/11603893>`_
* `Python gc 模块文档 <https://docs.python.org/2/library/gc.html>`_
* `Python gc 代码 <https://hg.python.org/cpython/file/tip/Modules/gcmodule.c>`_

面向对象编程
=======================

继承和组合
-----------------

多重继承
-----------------

模板和接口
-----------------

绑定
-----------------

修饰器
=======================

元类
=======================

匿名函数
=======================


在python中使用设计模式
=======================
