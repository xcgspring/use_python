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
| 在线演示网址`<https://www.tele3.cz/jbar/rest/rest.html>`_，网址的搭建过程`<https://www.tele3.cz/jbar/rest/about.html>`_。

字体相关语法
--------------------

==================== ==================== ======================
    **语法**               **输出**              **说明**
==================== ==================== ======================
\*斜体*              *斜体*                          
\**加粗**            **加粗**                         
\``内嵌``            ``内嵌``                     
==================== ==================== ======================

链接相关语法
--------------------

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
                            <p>
                                pypi_</p>
                            <p>
                                .. _pypi: https://pypi.python.org/pypi</p>
                        </td>
                        <td>
                            <a href="https://pypi.python.org/pypi">pypi</a></td>
                        <td>
                            外部链接1</td>
                    </tr>
                    <tr>
                        <td>
                            <p>
                                `python docs`_</p>
                            <p>
                                .. _`python docs`: http://docs.python.org</p>
                        </td>
                        <td>
                            <a href="http://docs.python.org">python docs</a></td>
                        <td>
                            外部链接2</td>
                    </tr>
                    <tr>
                        <td>
                            <p>
                                `python intro`_</p>
                            <p>
                                .. _`python intro`:</p>
                            <p>
                                python introducation</p>
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
                            <p>
                                `anonymous`__</p>
                            <p>
                                __ http://www.python.org/</p>
                        </td>
                        <td>
                            <a href="http://www.python.org/">anonymous</a></td>
                        <td>
                            匿名链接</td>
                    </tr>
                    <tr>
                        <td>
                            <p>
                                [1]_</p>
                            <p>
                                .. [1] this is a footnote</p>
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
                            <p>
                                [citation]_</p>
                            <p>
                                .. [citation] this is a citation</p>
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
--------------------

**标题**

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
						<p>
							parts</p>
						<p>
							###########</p>
						<p>
							chapters</p>
						<p>
							***********</p>
						<p>
							sections</p>
						<p>
							=========</p>
						<p>
							subsections</p>
						<p>
							------------</p>
						<p>
							subsubsections</p>
						<p>
							^^^^^^^^^^^^^^^</p>
						<p>
							paragraphs</p>
						<p>
							&quot;&quot;&quot;&quot;&quot;&quot;&quot;&quot;&quot;&quot;&quot;&quot;&quot;</p>
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
						&nbsp;</td>
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
						&nbsp;</td>
				</tr>
				<tr>
					<td>
						what<br />
						&nbsp;&nbsp;Definition lists associate a term with a definition.<br />
						how<br />
						&nbsp;&nbsp;The term is a one-line phrase, and the definition is one or more paragraphs or body elements, indented relative to the term. Blank lines are not allowed between term and definition.</td>
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
						&nbsp;</td>
				</tr>
				<tr>
					<td>
						&nbsp;</td>
					<td>
						&nbsp;</td>
					<td>
						&nbsp;</td>
				</tr>
				<tr>
					<td>
						&nbsp;</td>
					<td>
						&nbsp;</td>
					<td>
						&nbsp;</td>
				</tr>
				<tr>
					<td>
						&nbsp;</td>
					<td>
						&nbsp;</td>
					<td>
						&nbsp;</td>
				</tr>
			</tbody>
		</table>






















































