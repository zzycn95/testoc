# testoc
object-c

在ubuntu20.04上创建Object-C运行环境

使用这个教程必须安装

sudo apt install gobjc gobjc++ gnustep-make gnustep-devel

安装完后配置编译环境：

. /usr/share/GNUstep/Makefiles/GNUstep.sh

然后编写代码hello.h

然后使用观望编译的方式报错：

gcc `gnustep-config --objc-flags` -lgnustep-base hello.m -o hello

错误如下：

/test/object-c/hello.m:4：对‘objc_get_class’未定义的引用
/test/object-c/hello.m:4：对‘objc_msg_lookup’未定义的引用
/test/object-c/hello.m:4：对‘objc_msg_lookup’未定义的引用
/test/object-c/hello.m:5：对‘NSLog’未定义的引用
/test/object-c/hello.m:6：对‘objc_msg_lookup’未定义的引用
/tmp/ccFeqgkG.o：在函数‘__objc_gnu_init’中：
/test/object-c/hello.m:9：对‘__objc_exec_class’未定义的引用
/tmp/ccFeqgkG.o:(.data.rel+0x0)：对‘__objc_class_name_NSConstantString’未定义的引用
/tmp/ccFeqgkG.o:(.data.rel+0x8)：对‘__objc_class_name_NSAutoreleasePool’未定义的引用
collect2: error: ld returned 1 exit status

 网上搜了一下，解决方案就是如下：

gcc `gnustep-config --objc-flags` -Wl,--no-as-needed -lobjc -lgnustep-base hello.m -o hello.o

比原来多添加了-Wl,--no-as-needed -lobjc

最后使用 ./hello.o执行就可以了

————————————————
版权声明：本文为CSDN博主「葫芦娃二娃」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/hubbybob1/article/details/102815729