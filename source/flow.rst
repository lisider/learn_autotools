flow
=====
其实这个流程可以简化,也可以复杂
简化的流程可以简单到 只用 autoscan 和 autoconf  工具
复杂的流程要用到 autoscan autoheader aclocal automake autoconf 工具

流程越复杂,产出的架构越清晰,文件越分散


.. code-block:: shell

     第一次的流程


     1/
     手动 创建 源代码 ,手动创建Makefile.am

     2/
     autoscan
     
     3/
     mv configure.scan configure.ac
     
     4/
     autoheader
     
     5/
     手动 add AM_INIT_AUTOMAKE to configure.ac
     
     6/
     aclocal
     
     7/
     automake --add-missing --copy
     
     8/
     autoconf

     9/
     ./configure

     10/
     make

     11/
     make install
     

     ----


     修改过源码之后的流程
     
     autoscan
     
     手动update configure.ac (compare configure.scan with configure.ac)
     
     autoreconf


操作流程
---------

.. image:: _static/flow.jpg


从上图可以看出来,这个东西需要5个工具,需要修改configure.ac 和创建 Makefile.am


参考文档
--------

`autotools2`_
.. _`autotools2` : http://www.lugod.org/presentations/autotools/presentation/autotools.pdf
