libtool
=======


.. code-block:: shell

     /.
     /usr
     /usr/bin
     /usr/bin/libtoolize
     /usr/share
     /usr/share/aclocal
     /usr/share/aclocal/ltversion.m4
     /usr/share/aclocal/libtool.m4
     /usr/share/aclocal/ltsugar.m4
     /usr/share/aclocal/ltargz.m4
     /usr/share/aclocal/lt~obsolete.m4
     /usr/share/aclocal/ltoptions.m4
     /usr/share/libtool
     /usr/share/libtool/build-aux
     /usr/share/libtool/build-aux/install-sh
     /usr/share/libtool/build-aux/depcomp
     /usr/share/libtool/build-aux/compile
     /usr/share/libtool/build-aux/ltmain.sh
     /usr/share/libtool/build-aux/missing
     /usr/share/doc
     /usr/share/doc/libtool
     /usr/share/doc/libtool/NEWS.gz
     /usr/share/doc/libtool/THANKS.gz
     /usr/share/doc/libtool/AUTHORS
     /usr/share/doc/libtool/copyright
     /usr/share/doc/libtool/changelog.Debian.gz
     /usr/share/doc/libtool/README.Debian
     /usr/share/doc/libtool/README
     /usr/share/doc/libtool/TODO.gz
     /usr/share/man
     /usr/share/man/man1
     /usr/share/man/man1/libtoolize.1.gz
     /usr/share/libtool/build-aux/config.sub
     /usr/share/libtool/build-aux/config.guess


libtool 文件类型
----------------

.. code-block:: shell

     $ file /usr/bin/libtool
     /usr/bin/libtool: Bourne-Again shell script, ASCII text executable

libtool 的实质
--------------

.. code-block:: shell

     可以这么说,libool 是 对各个平台的不同工具链 构建 的 封装
     pkg-config 是gcc 选项 的封装

     在不同的平台上,编译过程和链接过程是不一样的
     不可以用同一个命令跑在多个系统上
     但是 libtool 封装了 各个系统 上的编译连接过程,然后就可以用
     libtool 的一条命令 ,运行在多个系统上 

     虽然封装了编译连接过程,但是并没有封装 编译器,所以编译器还需要指定

     另外,还需要 指定我们要做的 动作 ,链接还是编译

     另外,还需要指定我们要 做的动作的参数 
          1 编译什么文件,头文件位置  
          2 连接什么文件 ,连接成什么文件,依赖的库的 位置


     在命令执行的过程中,会生成一些 lo la 文件,需要我们 关注,这就是 2 过程中的参数



命令怎么键入
------------
.. code-block:: shell

     编译
     libtool --mode=compile gcc -g -O -c foo.c
     libtool --mode=compile --tag=CC mipsel-linux-gcc -g -I../include -c BTX.c
     连接1
     libtool --mode=link gcc -g -O -o libhello.la foo.o hello.o
     libtool --mode=link gcc -g -O -o libhello.la foo.lo hello.lo -rpath /usr/local/lib -lm
     连接2
     libtool --mode=link gcc -g -O -o hell main.o libhello.la


     编译的过程中 可以 有 .c 存在
     连接的过程中 只可以有 .la(库) .lo(中间文件) 存在,如果出现 .o 是不合法的

命令的执行过程
--------------
.. code-block:: shell

     编译的时候
     1.创建.libs

     2.编译了一个与位置无关（-fPIC）的obj文件。 放在 .lib中。

     3.编译了一个普通obj文件在本地。

     4.生成了 .lo

     连接的时候
     1.取出.lo 或者 .la文件进行解析

     2.生成 .la 文件 或者 可执行文件

