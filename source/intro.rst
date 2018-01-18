autotools是用来干什么的
=======================

building useful, solid and distribution-friendly packages

autotools是什么
=======================
GNU build chain



autotools包括什么
=======================

autoconf, automake, libtool, pkg-config, and so on.


autoconf 用来生成configure脚本

automake 用来 做什么的?

libtool 用来简化 链接选项的
     

pkg-config 也是用来简化编译连接选项的
     pkg-config looks in /usr/lib/pkgconfig, /usr/share/pkgconfig,/usr/local/lib/pkgconfig and /usr/local/share/pkgconfig

     PKG_CONFIG_PATH
     export PKG_CONFIG_PATH=/opt/gtk/lib/pkgconfig:$PKG_CONFIG_PATH
     一般编译源码的时候会生成 .pc文件,然后安装的时候安装到相应目录.

     使用的话,像下面这样子就可以了,但是有时候会出现一些问题,例如,pkg-config –cflags libcjson 显示为空,pkg-config –libs libcjson 

     cc program.c $(pkg-config --cflags --libs gnomeui)
     gcc -c `pkg-config --cflags glib-2.0` sample.c








参考文档
`autotools`_

.. _`autotools` : https://autotools.io/index.html
