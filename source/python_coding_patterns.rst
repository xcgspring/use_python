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

动态加载
=======================

Python通过 __import__ 函数支持动态加载模块， 类似于Java的反射机制。


return VS exception
=======================

property VS method
=======================

Unicode
=======================

线程和全局锁
=======================

垃圾回收机制
=======================

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