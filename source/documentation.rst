.. _`编写文档`:

================================
编写文档
================================

:Page Status: Development
:Last Reviewed: 

使用reStructuredText来编写文档，使用Sphinx来管理和发布文档。

reStructuredText
================

| reStructuredText是一个纯文本的标记语言，可被用于python内嵌文档编写，网页编写或者用来写文章。
| Python库docutils实现了对reStructuredText标记语言的解析支持，并能将其转化成其他常用的文档格式，如HTML，Latex，PDF

| 建议学习reStructuredText语法的同时不断练习以加深印象。
| `在线演示网址 <https://www.tele3.cz/jbar/rest/rest.html>`_ ， `网址的搭建过程 <https://www.tele3.cz/jbar/rest/about.html>`_ 。

字体相关语法
----------------

==================== ==================== ======================
    **语法**               **输出**              **说明**
==================== ==================== ======================
\*斜体*              *斜体*                          
\**加粗**            **加粗**                         
\``内嵌``            ``内嵌``                     
==================== ==================== ======================

链接相关语法
-----------------

.. raw:: html

            <table border="1" cellpadding="1" cellspacing="1" style="width: 500px;">
                <tbody>
                    <tr>
                        <td style="text-align: center;">
                            <strong>语法</strong></td>
                        <td style="text-align: center;">
                            <strong>输出</strong></td>
                        <td style="text-align: center;">
                            <strong>说明</strong></td>
                    </tr>
                    <tr>
                        <td>
                            `python &lt;http://www.python.org&gt;`_</td>
                        <td>
                            <a href="http://www.python.org">python</a></td>
                        <td>
                            内嵌外部链接</td>
                    </tr>
                    <tr>
                        <td>
                                pypi_<br />
                                .. _pypi: https://pypi.python.org/pypi<br />
                        </td>
                        <td>
                            <a href="https://pypi.python.org/pypi">pypi</a></td>
                        <td>
                            外部链接1</td>
                    </tr>
                    <tr>
                        <td>
                                `python docs`_<br />
                                .. _`python docs`: http://docs.python.org<br />
                        </td>
                        <td>
                            <a href="http://docs.python.org">python docs</a></td>
                        <td>
                            外部链接2</td>
                    </tr>
                    <tr>
                        <td>
                                `python intro`_<br />
                                .. _`python intro`:<br />
                                 python introducation<br />
                        </td>
                        <td>
                            <p>
                                <a href="#python-intro">python intro</a></p>
                            <p id="python-intro">
                                python introducation</p>
                        </td>
                        <td>
                            内部链接</td>
                    </tr>
                    <tr>
                        <td>
                                `anonymous`__<br />
                                __ http://www.python.org/<br />
                        </td>
                        <td>
                            <a href="http://www.python.org/">anonymous</a></td>
                        <td>
                            匿名链接</td>
                    </tr>
                    <tr>
                        <td>
                                [1]_<br />
                                .. [1] this is a footnote<br />
                        </td>
                        <td>
                            <p class="first">
                                <a class="footnote-reference" href="#id3" id="id2">[1]</a></p>
                            <table frame="void" id="id3" rules="none">
                                <tbody valign="top">
                                    <tr>
                                        <td>
                                            <a class="fn-backref" href="#id2">[1]</a></td>
                                        <td>
                                            this is a foot note</td>
                                    </tr>
                                </tbody>
                            </table>
                        </td>
                        <td>
                            脚注</td>
                    </tr>
                    <tr>
                        <td>
                                [citation]_<br />
                                .. [citation] this is a citation<br />
                        </td>
                        <td>
                            <p>
                                <a href="#citation" id="id4">[citation]</a></p>
                            <table frame="void" id="citation" rules="none">
                                <tbody valign="top">
                                    <tr>
                                        <td>
                                            <a class="fn-backref" href="#id4">[citation]</a></td>
                                        <td>
                                            this is a citation</td>
                                    </tr>
                                </tbody>
                            </table>
                        </td>
                        <td>
                            引用</td>
                    </tr>
                </tbody>
            </table>

段落相关语法
-----------------

**普通段落**

.. raw:: html

        <table border="1" cellpadding="1" cellspacing="1">
			<tbody>
				<tr>
					<td style="text-align: center;">
						<strong>语法</strong></td>
					<td style="text-align: center;">
						<strong>输出</strong></td>
					<td style="text-align: center;">
						<strong>说明</strong></td>
				</tr>
				<tr>
					<td>
						This is a paragraph.<br />
						<br />
						Paragraphs line up at<br />
						their left edges,<br />
						and are normally separated<br />
						by blank lines.</td>
					<td>
						This is a paragraph.<br />
						Paragraphs line up at their left edges, and are normally separated by blank lines.</td>
					<td>
						段落以空行分隔</td>
				</tr>
			</tbody>
		</table>


**标题**

.. raw:: html

		<table border="1" cellpadding="1" cellspacing="1" style="table-layout: fixed;">
			<tbody>
				<tr>
					<td style="width: 30%; text-align: center;">
						<strong>语法</strong></td>
					<td style="width: 30%; text-align: center;">
						<strong>输出</strong></td>
					<td style="width: 30%; text-align: center;">
						<strong>说明</strong></td>
				</tr>
				<tr>
					<td>
							parts<br />
							###########<br />
						<br />
							chapters<br />
							***********<br />
						<br />
							sections<br />
							=========<br />
						<br />
							subsections<br />
							------------<br />
						<br />
							subsubsections<br />
							^^^^^^^^^^^^^^^<br />
						<br />
							paragraphs<br />
							&quot;&quot;&quot;&quot;&quot;&quot;&quot;&quot;&quot;&quot;&quot;&quot;&quot;<br />
					</td>
					<td>
						<h1 style="text-align: center;">
							parts</h1>
						<h2 style="text-align: center;">
							chapters</h2>
						<h3>
							sections</h3>
						<h4>
							subsections</h4>
						<h5>
							subsubsections</h5>
						<h6>
							paragraphs</h6>
					</td>
					<td>
						<p>标题由底部（或底部和顶部）连续的一组ASCII非字母数字的字符标识， 标题级别自动分配，最先出现的标题级别较高， 推荐使用标识字符有"= - ` : ' " ~ ^ _ * + # < >"。</p>
                        <p>Sphinx推荐在python文档中使用如下的规则：</p>
                        <li># with overline, for parts</li>
                        <li>* with overline, for chapters</li>
                        <li>=, for sections</li>
                        <li>-, for subsections</li>
                        <li>^, for subsubsections</li>
                        <li>", for paragraphs</li>

                        </td>
				</tr>
			</tbody>
		</table>

**列表**

列表的开始和结束各需要一个空行，列表中间的空行是可有可无的

.. raw:: html

		<table border="1" cellpadding="1" cellspacing="1">
			<tbody>
				<tr>
					<td style="text-align: center;">
						<strong>语法</strong></td>
					<td style="text-align: center;">
						<strong>输出</strong></td>
					<td style="text-align: center;">
						<strong>说明</strong></td>
				</tr>
				<tr>
					<td>
						- This is item 1<br />
						- This is item 2</td>
					<td>
						<ul>
							<li>
								This is item 1</li>
							<li>
								This is item 2</li>
						</ul>
					</td>
					<td>
						Bullet Lists</td>
				</tr>
				<tr>
					<td>
						3. This is the first item<br />
						4. This is the second item<br />
						5. Enumerators are arabic numbers, single letters, or roman numerals<br />
						6. List items should be sequentially numbered, but need not start at 1 (although not all formatters will honour the first index).<br />
						#. This item is auto-enumerated</td>
					<td>
						<ol start="3">
							<li>
								This is the first item</li>
							<li>
								This is the second item</li>
							<li>
								Enumerators are arabic numbers, single letters, or roman numerals</li>
							<li>
								List items should be sequentially numbered, but need not start at 1 (although not all formatters will honour the first index).</li>
							<li>
								This item is auto-enumerated</li>
						</ol>
					</td>
					<td>
						Enumerated Lists</td>
				</tr>
				<tr>
					<td>
						what<br />
						  Definition lists associate a term with a definition.<br />
						how<br />
						  The term is a one-line phrase, and the definition is one or more paragraphs or body elements, indented relative to the term. Blank lines are not allowed between term and definition.</td>
					<td>
						<dl>
							<dt>
								<strong>what</strong></dt>
							<dd>
								Definition lists associate a term with a definition.</dd>
							<dt>
								<strong>how</strong></dt>
							<dd>
								The term is a one-line phrase, and the definition is one or more paragraphs or body elements, indented relative to the term. Blank lines are not allowed between term and definition.</dd>
						</dl>
					</td>
					<td>
						Definition Lists</td>
				</tr>
				<tr>
					<td>
						:Authors:<br />
						Tony J. (Tibs) Ibbs,<br />
						David Goodger<br />
						<br />
						(and sundry other good-natured folks)<br />
						<br />
						:Version: 1.0 of 2001/08/08<br />
						:Dedication: To my father.</td>
					<td>
						<strong>Authors:</strong> Tony J. (Tibs) Ibbs, David Goodger<br />
						(and sundry other good-natured folks)<br />
						<strong>Version:</strong> 1.0 of 2001/08/08<br />
						<strong>Dedication:</strong> To my father.</td>
					<td>
						Field Lists</td>
				</tr>
				<tr>
					<td>
						-a            command-line option &quot;a&quot;<br />
						-b file       options can have arguments<br />
						              and long descriptions<br />
						--long        options can be long also<br />
						--input=file  long options can also have<br />
						              arguments<br />
						/V            DOS/VMS-style options too</td>
					<td>
						<table border="0" width="100%">
							<tbody valign="top">
								<tr>
									<td width="30%">
										-a</td>
									<td>
										command-line option &quot;a&quot;</td>
								</tr>
								<tr>
									<td>
										-b <i>file</i></td>
									<td>
										options can have arguments and long descriptions</td>
								</tr>
								<tr>
									<td>
										--long</td>
									<td>
										options can be long also</td>
								</tr>
								<tr>
									<td>
										--input=<i>file</i></td>
									<td>
										long options can also have arguments</td>
								</tr>
								<tr>
									<td>
										/V</td>
									<td>
										DOS/VMS-style options too</td>
								</tr>
							</tbody>
						</table>
					</td>
					<td>
						Option Lists</td>
				</tr>
			</tbody>
		</table>

**块**

块中的特殊字符不会被解析和替代， 所有的特殊字符，空格和换行符会被保留。

.. raw:: html

		<table border="1" cellpadding="1" cellspacing="1" style="table-layout: fixed;">
			<tbody>
				<tr>
					<td style="width: 40%; text-align: center;">
						<strong>语法</strong></td>
					<td style="width: 40%; text-align: center;">
						<strong>输出</strong></td>
					<td style="width: 20%; text-align: center;">
						<strong>说明</strong></td>
				</tr>
				<tr>
					<td>
						A paragraph containing only two colons<br />
						indicates that the following indented<br />
						or quoted text is a literal block.<br />
						<br />
						::<br />
						<br />
						Whitespace, newlines, blank lines, and<br />
						all kinds of markup (like *this* or<br />
						\this) is preserved by literal blocks.<br />
						<br />
						The paragraph containing only &#39;::&#39;<br />
						will be omitted from the result.<br />
						<br />
						The ``::`` may be tacked onto the very<br />
						end of any paragraph. The ``::`` will be<br />
						omitted if it is preceded by whitespace.<br />
						The ``::`` will be converted to a single<br />
						colon if preceded by text, like this::<br />
						<br />
						It&#39;s very convenient to use this form.<br />
						<br />
						Literal blocks end when text returns to<br />
						the preceding paragraph&#39;s indentation.<br />
						This means that something like this<br />
						is possible::<br />
						<br />
						We start here<br />
						and continue here<br />
						and end here.<br />
						<br />
						Per-line quoting can also be used on<br />
						unindented literal blocks::<br />
						<br />
						&gt; Useful for quotes from email and<br />
						&gt; for Haskell literate programming.</td>
					<td>
						<p>
							A paragraph containing only two colons indicates that the following indented or quoted text is a literal block.</p>
						<pre>
  Whitespace, newlines, blank lines, and
  all kinds of markup (like *this* or
  \this) is preserved by literal blocks.

  The paragraph containing only &#39;::&#39;
  will be omitted from the result.</pre>
						<p>
							The :: may be tacked onto the very end of any paragraph. The :: will be omitted if it is preceded by whitespace. The :: will be converted to a single colon if preceded by text, like this:</p>
						<pre>
  It&#39;s very convenient to use this form.</pre>
						<p>
							Literal blocks end when text returns to the preceding paragraph&#39;s indentation. This means that something like this is possible:</p>
						<pre>
      We start here
    and continue here
  and end here.</pre>
						<p>
							Per-line quoting can also be used on unindented literal blocks:</p>
						<pre>
  &gt; Useful for quotes from email and
  &gt; for Haskell literate programming.</pre>
					</td>
					<td>
						<strong>段落块</strong><br />
						两个冒号加一个空行后面所有的缩进的段落都是块</td>
				</tr>
				<tr>
					<td>
						| Line blocks are useful for addresses,<br />
						| verse, and adornment-free lists.<br />
						|<br />
						| Each new line begins with a<br />
						| vertical bar (&quot;|&quot;).<br />
						| Line breaks and initial indents<br />
						| are preserved.<br />
						| Continuation lines are wrapped<br />
						portions of long lines; they begin<br />
						with spaces in place of vertical bars.</td>
					<td>
						Line blocks are useful for addresses,<br />
						verse, and adornment-free lists.<br />
						<br />
						Each new line begins with a<br />
						vertical bar (&quot;|&quot;).<br />
						Line breaks and initial indents<br />
						are preserved.<br />
						Continuation lines are wrapped<br />
						portions of long lines;<br />
						they begin with spaces in place<br />
						of vertical bars.</td>
					<td>
						<strong>行块</strong></td>
				</tr>
			</tbody>
			<tbody>
			</tbody>
		</table>

**注释**

没有有效标记(如脚注)的直解标记(.. )文本块就是注释(`参考 <http://docutils.sourceforge.net/docs/ref/rst/restructuredtext.html#comments>`_) 例如:

| .. This is a comment.


可以用缩进文本来进行多行注释:

::

 ..
   This whole indented block
   is a comment.

   Still in the comment.


表格语法
--------------------

没有好的编辑器支持的话，建议不要使用reStructureText的表格，写起来很费时间。


指令语法
--------------------

指令是reStructuredText用来在不改变/新增已有语法的基础上，扩展新的特性的一种机制。

`reStructuredText标准指令文档 <http://docutils.sourceforge.net/docs/ref/rst/directives.html>`_ 罗列了所有的标准指令

其他的指令由各自的解析器自己定义，比如sphinx就支持很多 `自定义的指令 <http://sphinx-doc-zh.readthedocs.org/en/latest/markup/index.html>`_ 

指令语法示意:: 

    +-------+------------------+
    | ".. " | 指令类型 "::" 指令 |
    +-------+ 块               |
            |                  |
            +------------------+
            
指令块由指令符后面所有缩进内容组成，指令块可以包含三部分：

1. Directive arguments
2. Directive options
3. Directive content

Directive arguments和Directive options紧接着指令。Directive content和它们之间用空行分隔。

不同的指令对指令块的要求不同，如果提供的指令块不符合要求，会导致错误

下面介绍一些常用的标准指令和sphinx自定义指令。

        
reStructuredText标准指令
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

提醒指令
"""""""""""

`提醒指令 <http://docutils.sourceforge.net/docs/ref/rst/directives.html#specific-admonitions>`_ ，包含"attention", "caution", "danger", "error", "hint", "important", "note", "tip", "warning", "admonition"

**示例**:: 

 .. attention::
  Attention Please!
  
**输出** ：

.. attention::
 Attention Please!
 
image指令
"""""""""""""

图片指令向输出中插入指定图片

**示例**:: 

 .. image:: images/happy_dog.jpg
   :height: 200px
   :width: 300 px
   :scale: 50 %
   :alt: 快乐的狗狗
  
**输出** ：

.. image:: images/happy_dog.jpg
   :height: 200px
   :width: 300 px
   :scale: 50 %
   :alt: 快乐的狗狗


**raw指令**
""""""""""""""""


sphinx自定义指令
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^















