# flashimg
========

Flashimg is a tool used to create and handle flash image file. Usefull for QEMU.

[git://gitorious.org/flashimg/flashimg.git](git://gitorious.org/flashimg/flashimg.git)

以下内容参考博客  
https://blog.csdn.net/qq_36243846/article/details/73321830


## 1.关于flashimg

Flashimg是一个强大的工具，是一个由网友FabriceJouhaud 开发的软件，可以很快捷地生成NAND或NOR镜像文件。在不了解flash内部组成和操作原理的情况下，这个软件就可以生成你所想要的大小的镜像文件。

## 2.使用flashimg
首先下载flashimg：

git clone https://github.com/pleasecallmekaige/flashimg.git

在linux系统编译安装：

①     ./autogen.sh

②     ./configure

③     make

④     sudo make install

编译成功后，出现一个可执行文件flashimg

要生成NAND或NOR镜像文件，可以先把之前Buildroot替我们生成的三个文件：u-boot.bin, uImage和rootfs.jffs2 拷贝到flashimg文件夹下，生成NAND或NOR镜像文件，这三个文件是bootloader的镜像，u-boot格式的（用mkimage命令生成的）Linux内核镜像，jffs2格式的根文件系统镜像（这个工程默认用的是jffs2根文件系统）源码编译生成出来的文件。把文件拷贝到flashimg目录下后，就可以执行flashimg了。

$    flashimg -s64M -t nand-f nand.bin -p uboot.part -w boot,u-boot.bin -w kernel,uImage -wroot,rootfs.jffs2 -z 512

$    flashimg-s 2M -t nor-f nor.bin -p uboot.part -w boot,u-boot.bin -w kernel,uImage -wroot,rootfs.jffs2

其中

-s                 镜像文件的大小

-t                  类型指定nand或nor

-f                 镜像文件

-p                 指定名字，偏移和大小

-w                指定生成镜像的源文件

-z                 页大小