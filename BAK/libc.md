ld-linux.so查找共享库的顺序

Glibc安装的库中有一个为ld-linux.so.X，其中X为一个数字，在不同的平台上名字也会不同。可以用ldd查看：

#ldd /bin/cat
linux-gate.so.1 => (0x00bfe000)
libc.so.6 => /lib/libc.so.6 (0x00a4a000)
/lib/ld-linux.so.2 (0x00a28000)

最后一个没有=>的就是。其中第一个不是实际的库文件，你是找不到的，它是一个虚拟库文件用于和kernel交互。

ld-linux.so是专门负责寻找库文件的库。以cat为例，cat首先告诉ld-linux.so它需要libc.so.6这个库文件，ld-linux.so将按一定顺序找到libc.so.6库再给cat调用。

那ld-linux.so又是怎么找到的呢？其实不用找，ld-linux.so的位置是写死在程序中的，gcc在编译程序时就写死在里面了。Gcc写到程序中ld-linux.so的位置是可以改变的，通过修改gcc的spec文件。
运行时，ld-linux.so查找共享库的顺序

（1）ld-linux.so.6在可执行的目标文件中被指定，可用readelf命令查看
（2）ld-linux.so.6缺省在/usr/lib和lib中搜索；当glibc安装到/usr/local下时，它查找/usr/local/lib
（3）LD_LIBRARY_PATH环境变量中所设定的路径
（4）/etc/ld.so.conf（或/usr/local/etc/ld.so.conf）中所指定的路径，由ldconfig生成二进制的ld.so.cache中
编译时，ld-linux.so查找共享库的顺序

（1）ld-linux.so.6由gcc的spec文件中所设定
（2）gcc --print-search-dirs所打印出的路径，主要是libgcc_s.so等库。可以通过GCC_EXEC_PREFIX来设定
（3）LIBRARY_PATH环境变量中所设定的路径，或编译的命令行中指定的-L/usr/local/lib
（4）binutils中的ld所设定的缺省搜索路径顺序，编译binutils时指定。（可以通过“ld --verbose | grep SEARCH”来查看）
（5）二进制程序的搜索路径顺序为PATH环境变量中所设定。一般/usr/local/bin高于/usr/bin
（6）编译时的头文件的搜索路径顺序，与library的查找顺序类似。一般/usr/local/include高于/usr/include