.. index:: ! fonts

文字
====

前面几节说了GMT中如何画线条以及如何填充颜色，这节说说文字的那些事。

文字，或者称文本或字符串，主要由三个属性控制：文字大小、字体类型、填充色。三个属性之间用逗号分隔，即 ``<size>,<fonttype>,<fill>`` 。三者均是可选的，但先后顺序不可乱。若其中任意一个属性被省略，则使用该属性的默认值或上一次的设置值。

文字大小
--------

文字大小，可以理解成字号，用数字加单位表示。在不指定单位的情况下默认单位为 ``p`` ，也可加上 ``c`` 、 ``p`` 或者 ``i`` 显式指定单位，比如 ``15p`` 。

字体类型
--------

字体类型控制了文字使用哪一种字体。大多数PostScript解释器都内置35种标准字体，GMT默认支持且只支持这35种标准字体。若你使用的PS解释器不支持其中某些字体，则会自动用默认字体（一般是Courier）替换需要的字体。

下图给出了GMT支持的35种字体的列表：

.. figure:: /images/GMT_fonts.*
   :width: 600 px
   :align: center

   GMT中的35种PS标准字体

GMT中可以用字体名（区分大小写）或对应的字体编号来指定字体。上图中给出了每种字体的字体编号以及字体名称。每个字体名称使用的是自己相对应的字体，所以可以从图中直观地看出不同字体的区别。

图中大多数字体都很直观，比较特别的字体有两个，Symbol（12号）和ZapfDingbats（34号），在 :doc:`special-fonts` 中会专门介绍。

填充色
------

可以为文字指定颜色或图案，也就是常说的文字颜色，见 :doc:`fill` 一节。

描边
----

在给文字指定填充色的同时，可以在填充色 ``<fill>`` 后加上 ``=<pen>`` 来指定文本轮廓（即描边）的画笔属性。 ``<pen>`` 的用法见 :doc:`pen` 一节。比如 ``red=2p,blue`` 表示将文字填充为红色，并使用宽度为 ``2p`` 的蓝色线条给文字描边。若填充色 ``<fill>`` 为 ``-`` ，则不对文字做填充，即实现空心文字的效果。

使用 ``=<pen>`` 语法绘制文本轮廓时，轮廓线条有一半宽度位于文字外部，另一半宽度会遮住字体。为了避免这一现象，可以使用 ``=~<pen>`` 语法，此时在绘制文字轮廓时只绘制文字外部的半个线宽的线条。

示例
----

下图给出了几种指定文本属性的方式：

.. figure:: /images/GMT_text_examples.*
   :width: 600 px
   :align: center

   GMT文本属性示例

从下往上，一一解释一下：

#. 字号为 ``30p`` ，其余使用默认值
#. 字号为 ``30p`` ，使用8号字体
#. 字号为 ``30p`` ，8号字体，颜色为红色
#. 字号为 ``30p`` ，5号字体，字色为蓝色，用宽度为 ``1p`` 的黑色实线描边
#. 与前一个相同，唯一区别在于字色为 ``-`` ，相当于透明色，产生空心文字

读者可以将下面命令中 ``-F+f`` 后的 ``<font>`` 修改为不同的值以帮助理解本节的内容::

    echo 2.5 0.5 TEXT | gmt pstext -R0/5/0/1 -JX15c/2c -F+f<font> > text.ps
