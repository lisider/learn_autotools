build
==========================
拿到autotools源码怎么编译

prepare
--------------------------

.. code-block:: shell

     查看所属用户
     解压


configure
--------------------------

.. code-block:: shell

     ./configure 的时候 需要 Makefile.in 和 config.h.in(不是必须的)
     ./configure 的时候 会产生 Makefile  和 config.h
     configure 是一个脚本文件

     ./configure 做了 什么
     该脚本将运行一些测试来判断一些系统相关的变量
     检测你的操作
     系统的特殊设置
     最后在制做树中创建一些文件以记录它找到了什么

     一般用 ./configure VAR=xxx 的格式执行
     不会修改环境变量,只会对产出的 Makefile config.h  有影响
     所以没有必要 用 sudo 来执行


     ./configure 的时候 可以指定 目标安装文件夹 --prefix=path
     默认为 /usr/local/

     $./configure  --help |grep prefix -3
           --srcdir=DIR        find the sources in DIR [configure dir or `..']

     Installation directories:
       --prefix=PREFIX         install architecture-independent files in PREFIX
                               [/usr/local]
       --exec-prefix=EPREFIX   install architecture-dependent files in EPREFIX
                               [PREFIX]

     By default, `make install' will install all the files in
     `/usr/local/bin', `/usr/local/lib' etc.  You can specify
     an installation prefix other than `/usr/local' using `--prefix',
     for instance `--prefix=$HOME'.


make
--------
.. code-block:: shell

     一般只会修改该文件夹下的内容
     不会影响其他的
     一般只会编译成 .o .a .so .la 文件


make install
------------
.. code-block:: shell

     这个需要根据权限来决定是否要加上 sudo 权限
     因为要复制一些文件到 目标文件夹中去
     如果目标文件夹当前用户没有写入的权限,就需要提升权限

     $ls -l /usr/  |grep local
     drwxr-xr-x  14 root root  4096 12月 26 11:37 local

target else
------------

.. code-block:: shell

     
     　　在符合GNU Makefiel惯例的Makefile中,包含了一些基本的预先定义的操作：
     make
     　　根据Makefile编译源代码,连接,生成目标文件,可执行文件.
     make clean
     　　清除上次的make命令所产生的object文件（后缀为".o"的 文件）及可执行文件.
     make install
     　　将编译成功的可执行文件安装到系统目录中,一般为/usr/local/bin目录.
     make dist
     　　产生发布软件包文件（即distribution package）.这个命令将会将可执行文件及相关文件打包成一个tar.gz压缩的文件用来作为发布软件的软件包.
     　　它会在当前目录下生成一个名字类似"PACKAGE-VERSION.tar.gz"的文件.PACKAGE和VERSION,是我们在configure.ac中定义的AC_INIT([FULL-PACKAGE-NAME], [VERSION], [BUG-REPORT-ADDRESS]).
     make distcheck
     　　生成发布软件包并对其进行测试检查,以确定发布包的正确性.
     
