autotools是用来干什么的
=======================

building useful, solid and distribution-friendly packages

autotools 并不能帮你增强你的软件的移植性,那 useful solid distribution-friendly 体现在哪里?
他可以 帮你做在各个平台上 编译的过程,但是具体编译哪些东西,用什么选项还是你说了算
他只是构建一个 在 某个平台上合法的 makefile

autotools 封装了一个软件包,那么这个软件包的编译流程都是一样的
./configure;make;make install

autotools是什么
------------------
GNU build chain



autotools包括什么
-------------------

autoconf, automake, libtool, pkg-config, and so on.


autoconf 用来生成configure脚本

automake 用来 生成Makefile.in

libtool 用来 包装gcc 的
     
pkg-config 也是用来包装 编译连接选项的

autotools的作用
-------------------



autoconf automake 在 \*nix 混战时代是 非常有效的手段,但随着系统的逐步统一,这写跨平台的优势已经很小了

例如我直接写 Makefile 就可以 在各个平台使用了,不用使用autoconf automake

不过 autoconf 做出来的 configure 文件 是大多数开源代码中的标配
还有部分源码已经转向cmake 管理

autoconf automake 封装了 各个平台的 项目级别的编译链接过程
libtool 封装了 各个平台的 文件级别 的 编译连接过程
pkg-config 封装了 各个平台的 编译过程级别 的 编译选项

autoconf 和 automake 是单独一体的, 但是也可以在 makefile.am 中用 pkg-config 命令的输出作为编译链接选项

libtool 可以包含 pkg-config

autoconf 和 automake 不能包含 libtool



参考文档
--------
`autotools`_

.. _`autotools` : https://autotools.io/index.html
