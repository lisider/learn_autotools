files_todo
==========

需要创建的文件就两个
configure.ac 
Makefile.am

content in configure.ac
-----------------------


.. code-block:: shell

     里面有什么内容
     
     为什么只添加一个 AM_INIT_AUTOMAKE 就可以了
     
     会有一些 AC_CHECK_
     AC_PROG_CC 检查 C编译器
     
     AC_OUTPUT(FILE)这个宏是我们要输出的Makefile的名字.
     
     宏的顺序没有规定,只要在 AC_INIT宏和AC_OUTPUT宏 中间就行
     
     
     我们在使用automake时,实际上还需要用到其他的一些宏,但我们可以用aclocal来帮我们自动产生.执行aclocal后我们会得到aclocal.m4文件.
     
     
     configure.scan包含了系统配置的基本选项,里面都是一些宏定义.我们需要将它改名为configure.ac。
     autoconf是用来产生configure文件的.configure是一个脚本,它能设置源程序来适应各种不同的操作系统平台,
     并且根据不同的系统来产生合适的Makefile,从而可以使你的源代码能在不同的操作系统平台上被编译出来.
     configure.ac文件的内容是一些宏,这些宏经过autoconf处理后会变成检查系统特性、环境变量、软件必须的参数的shell脚本.
     configure.ac文件中的宏的顺序并没有规定,但是你必须在所有宏的最前面和最后面分别加上AC_INIT宏和AC_OUTPUT宏.
     在 configure.ac中：
     #号表示注释,这个宏后面的内容将被忽略.
     AC_INIT([FULL-PACKAGE-NAME], [VERSION], [BUG-REPORT-ADDRESS])这个宏定义了软件的名称和信息。
     (FULL-PACKAGE-NAME为软件名，VERSION为软件的版本号，BUG-REPORT-ADDRESS为bug的报告地址，一般为软件作者的邮箱）。
     当你使用make dist命令时,它会给你生成一个类似helloworld-1.0.tar.gz的软件发行包,其中就有对应的软件包的名字和版本号.
     AM_INIT_AUTOMAKE这个宏需要自己进行添加，它是automake所必备的宏。新版本中该宏不需要任何参数。
     AC_PROG_CC这个宏将检查系统所用的C编译器.
     产生了configure.ac和aclocal.m4两个宏文件后,我们就可以使用autoconf来产生configure文件了。


content in Makefile.am
-----------------------
.. code-block:: shell

     Makefile.am是用来生成Makefile.in的,需要你手工书写.Makefile.am中定义了一些内容：
     AUTOMAKE_OPTIONS
     　　这个是automake的选项.在执行automake时,它会检查目录下是否存在标准GNU软件包中应具备的各种文件,
         例如AUTHORS.ChangeLog.NEWS等文件.我们将其设置成foreign时,automake会改用一般软件包的标准来检查.


     bin_PROGRAMS
     　　这个是指定我们所要产生的可执行文件的文件名.如果你要产生多个可执行文件,那么在各个名字间用空格隔开.
     helloworld_SOURCES
     　　这个是指定产生"helloworld"时所需要的源代码.如果它用到了多个源文件,那么请使用空格符号将它们隔开.
         比如需要helloworld.h,helloworld.c那么请写成:helloworld_SOURCES= helloworld.h helloworld.c.
     　　如果你在 bin_PROGRAMS定义了多个可执行文件,则对应每个可执行文件都要定义相对的filename_SOURCES.
     _LDADD
     _LDFLAGS
     _CFLAGS


configure.ac 语法
-----------------
M4sh
     基于sh和宏语言M4


.. code-block:: shell

     AS_IF（[TEST1]，[TRUE]，[TEST2]，[TRUE2]，[FALSE]）


Makefile.am语法
-------------------

.. code-block:: shell

     目前不知道

