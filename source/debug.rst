.. _`python debug`:

=========================
python debug
=========================

:Page Status: Development
:Last Reviewed:


pdb
====

python自带的调试器,使用 ``python -m pdb myscript.py`` 或者 ``import pdb; pdb.set_trace()`` 进入调试模式(post-mortem debugging)

debug python code with gdb
==========================

pdb可以解决大部分python调试的需求,但是在一些复杂场景下,需要更强大的工具.
 - 调试正在运行的process
 - 调试可能hng的程序
 - 调试多线程

参考::

  https://wiki.python.org/moin/DebuggingWithGdb

remote debug
============

remote debug一般是IDE中提供的功能, 对于pycharm, 参考::

  https://www.jetbrains.com/help/pycharm/2017.1/remote-debugging.html#6

