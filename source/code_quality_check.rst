.. _`code quality check`:

=========================
python代码质量
=========================

:Page Status: Development
:Last Reviewed: 


python编码风格建议
=========================

参见 `Python guide, Code Style <http://docs.python-guide.org/en/latest/writing/style/>`_

.. note::

    关于使用返回值还是使用异常的建议：
    
    1. 我们应该对使用返回值的情景和使用异常的情景进行区分，使用返回值来表达函数的状态是不推荐的，会导致上层编码风格的混乱
    2. 只使用返回值来传递数据，如果函数没有想要返回的值，尽量不要在函数中使用return，python会默认返回None
    3. 使用具体的异常类型，比如built-in的 ``ValueError``, ``AttributeError``， 不要使用 ``Exception``， 如果需要自定义异常，将自定义的异常统一放到一个模块中，这样上层代码能方便访问你的自定义异常
    4. 尽量统一在上层处理异常，中间层尽量不处理异常，让异常扩散到统一处理异常的地方

python编码检查工具
=========================

`pylint <https://pypi.python.org/pypi/pylint>`_
--------------------------------------------------

使用 `pylint <https://pypi.python.org/pypi/pylint>`_ 相当简单，参见 `A Beginner’s Guide to Code Standards in Python - Pylint Tutorial <http://docs.pylint.org/tutorial.html>`_

.. note::

    `pylint <https://pypi.python.org/pypi/pylint>`_ 的默认设置有时候太严格了，我们可以通过创建pylint的configure文件来声明我们需要enable/disable哪些规则
    
    1. 首先，我们生成一份sample configure文件， ``pylint --generate-rcfile sample_config``
    2. 在文件中找到 ``[MESSAGES CONTROL]`` 段，设置 ``enable=`` ``disable=`` 为需要打开/关闭的规则，规则列表见 `http://docs.pylint.org/features.html#pylint-checkers-options-and-switches`
    3. configure文件需要放到合适的位置， 当前文件夹下的 *pylintrc* 文件 > 环境变量 `PYLINTRC` 指明的文件 > 用户目录下的 *.pylintrc* 文件 > */etc/pylintrc*

`landscape <https://landscape.io/>`_
---------------------------------------------------

一个python代码质量检查网站，对于开源工程是免费的。如果你的工程是一个host在GitHub上的开源的python工程，这个网站是一个很好的代码质量检查工具。

参考它的文档： `https://docs.landscape.io/#`
