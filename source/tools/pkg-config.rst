pkg-config
==========


.. code-block:: shell

     /.
     /usr
     /usr/share
     /usr/share/aclocal
     /usr/share/aclocal/pkg.m4
     /usr/share/man
     /usr/share/man/man1
     /usr/share/man/man1/pkg-config.1.gz
     /usr/share/pkgconfig
     /usr/share/pkg-config-dpkghook
     /usr/share/doc
     /usr/share/doc/pkg-config
     /usr/share/doc/pkg-config/README
     /usr/share/doc/pkg-config/copyright
     /usr/share/doc/pkg-config/changelog.Debian.gz
     /usr/share/doc/pkg-config/pkg-config-guide.html
     /usr/share/doc/pkg-config/NEWS.gz
     /usr/share/doc/pkg-config/AUTHORS
     /usr/share/pkg-config-crosswrapper
     /usr/lib
     /usr/lib/pkgconfig
     /usr/lib/pkg-config.multiarch
     /usr/bin
     /usr/bin/x86_64-pc-linux-gnu-pkg-config
     /usr/bin/pkg-config
     /etc
     /etc/dpkg
     /etc/dpkg/dpkg.cfg.d
     /etc/dpkg/dpkg.cfg.d/pkg-config-hook-config

这个东西可以做什么
------------------

生成编译选项 和 连接选项


怎么做
--------

.. code-block:: shell
     
     常用过的选项就这两个

     $ pkg-config  --cflags lua5.2 
     -I/usr/include/lua5.2
     $ pkg-config  --libs lua5.2       
     -llua5.2  

     $ pkg-config --cflags zlib 
     -I/usr/local/include  
     $ pkg-config --libs zlib 
     -L/usr/local/lib -lz  

     更实际的用户 是 以 
     $(pkg-config  --cflags lua5.2) 或者 
     `pkg-config  --cflags lua5.2`
     加载到命令行中运行
     gcc -c test.c `pkg-config  --cflags lua5.2` -o test.o 
     gcc test.o main.o `pkg-config  --libs lua5.2`

     或者 Makefile 中添加
     CFLAGS += `pkg-config --cflags sqlite3`
     LDFLAGS += `pkg-config --libs sqlite3`

命令执行的过程
--------------

.. code-block:: shell

     pkg-config  option xxx

     解析 xxx.pc文件 


.. code-block:: shell

     xxx.pc 在哪里找

     标准目录下的 pkgconfig 里面
     一般编译源码的时候会生成 .pc文件,然后安装的时候安装到相应目录.

     
     系统中有 这么多 pkgconfig
     $ locate pkgconfig |xargs file |awk '/directory/ {print $1}' | sed 's/://'
     /usr/lib/pkgconfig
     /usr/lib/i386-linux-gnu/pkgconfig
     /usr/local/lib/pkgconfig
     /usr/share/pkgconfig



     pkg-config looks in 
     /usr/lib/pkgconfig
     /usr/share/pkgconfig
     /usr/local/lib/pkgconfig
     /usr/local/share/pkgconfig

     PKG_CONFIG_PATH
     export PKG_CONFIG_PATH=/opt/gtk/lib/pkgconfig:$PKG_CONFIG_PATH

.. code-block:: shell

     xxx.pc 文件的内容

     
     示例1:
     prefix=/usr/local                                                                   
     exec_prefix=${prefix}                                                               
     libdir=${exec_prefix}/lib                                                           
     sharedlibdir=${libdir}                                                              
     includedir=${prefix}/include                                                     
                                                                                      
     Name: xxx                                                                        
     Description: xxx compression library                                             
     Version: 1.2.8                                                                   
                                                                                      
     Requires:                                                                        
     Libs: -L${libdir} -L${sharedlibdir} -lz                                          
     Cflags: -I${includedir} 


     man手册中的示例:
     Here is an example file:
     # This is a comment
     prefix=/home/hp/unst   # this defines a variable
     exec_prefix=${prefix}  # defining another variable in terms of the first
     libdir=${exec_prefix}/lib
     includedir=${prefix}/include
     
     Name: GObject                            # human-readable name
     Description: Object/type system for GLib # human-readable description
     Version: 1.3.1
     URL: http://www.gtk.org

     Requires: glib-2.0 = 1.3.1
     Conflicts: foobar <= 4.5
     Libs: -L${libdir} -lgobject-1.3
     Libs.private: -lm
     Cflags: -I${includedir}/glib-2.0 -I${libdir}/glib/include

