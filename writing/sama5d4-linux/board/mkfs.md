# SAMA5D4 Xplained Ultra 4 - 根文件系统制作


## 概述

所谓制作根文件系统，就是创建各种目录，并在里面创建各种文件。比如在 /bin、/sbin 目录下存放各种可执行程序，在 /etc目录下存放配置文件，在 /lib 目录下存放库文件。busybox 主要用来创建/bin、/sbin等目录下的可执行文件，如命令行下经常使用的命令ls、mv、cp等。


## 使用 busybox 构建 /bin、/sbin、linuxrc

从以下网站下载 busybox 源码，当前最新版本是 1.23.2：

[www.busybox.net](www.busybox.net)

```
$ make menuconfig
$ make CROSS_COMPILE=arm-none-linux-gnueabi- ARCH=arm
$ make install make CROSS_COMPILE=arm-none-linux-gnueabi- ARCH=arm
```

将 install 目录修改为 ../rootfs

完成后，将在 rootfs 目录内建立 bin、sbin、usr 文件夹和 linuxrc 链接文件，形成了根文件系统的。


## 添加 lib、usr/lib 目录

lib、usr/lib 目录内的文件从交叉编译器内拷贝：
```
cp -r ~/tools/arm-none-linux-gnueabi-4.7.2/arm-none-linux-gnueabi/libc/lib ./

mkdir usr/lib
cp -a ~/tools/arm-none-linux-gnueabi-4.7.2/arm-none-linux-gnueabi/libc/usr/lib/*.so* ./usr/lib/
cp -a ~/tools/arm-none-linux-gnueabi-4.7.2/arm-none-linux-gnueabi/libc/usr/lib/*.a* ./usr/lib/
```

## 添加 etc 目录

将 busybox 源码目录内 examples/bootfloopy 内 的 etc 目录拷贝过来
```
cp -rf ../busybox-1.23.2/examples/bootfloppy/etc/ ./
chmod a+x etc/init.d/rcS
```

1 修改 inittab

```
::sysinit:/etc/init.d/rcS
::respawn:-/bin/sh
tty2::askfirst:-/bin/sh
::ctrlaltdel:/bin/umount -a -r
```

修改为：

```
::sysinit:/etc/init.d/rcS
#::respawn:-/bin/login
console::askfirst:-/bin/sh
::ctrlaltdel:/bin/umount -a -r
```

或

```
::sysinit:/etc/init.d/rcS
::respawn:-/bin/login
#console::askfirst:-/bin/sh
::ctrlaltdel:/bin/umount -a -r
```

两者的区别是：前者开机免登陆，直接打开shell；后者开机需要登陆。

2 修改 fstab

3 修改 init.d/rcS

4 修改 profile

5 拷贝虚拟机上的/etc/passwd, /etc/group, /etc/shadow到rootfs/etc下
```
cp /etc/passwd etc
cp /etc/group etc
sudo cp /etc/shadow etc
```

## 添加 dev 目录及基本设备文件

```

```

## 添加其它目录

```
mkdir proc mnt tmp sys root
```


## 制作文件系统镜像

```shell
# !/bin/sh

PATH_ROOTFS=$PWD/../rootfs
PATH_IMAGES=$PWD/../images
IMG_NAME=root.bin


echo " _____________________________________________________________________ "
echo "|                                                                     |"
echo "| Please confirm there are nothing in the following directories (Y/n):|"
echo "| (not including README)                                              |"
echo "|     opt/norman opt/data                                             |"
echo "|_____________________________________________________________________|"

read confirm

case $confirm in
    n|N)
    echo "do nothing"
    exit 1
    ;;
esac


echo "making image root.bin"

if [ ! -d $PATH_ROOTFS/sys ]; then
    sudo mkdir $PATH_ROOTFS/sys
fi

if [ ! -d $PATH_ROOTFS/dev ]; then
    sudo mkdir $PATH_ROOTFS/dev
fi

if [ ! -d $PATH_ROOTFS/tmp ]; then
    sudo mkdir $PATH_ROOTFS/tmp
fi

if [ ! -d $PATH_ROOTFS/proc ]; then
    sudo mkdir $PATH_ROOTFS/proc
fi

if [ ! -d $PATH_ROOTFS/home ]; then
    sudo mkdir $PATH_ROOTFS/home
fi

if [ ! -d $PATH_ROOTFS/mnt ]; then
    sudo mkdir $PATH_ROOTFS/mnt
fi

if [ ! -d $PATH_ROOTFS/sddisk ]; then
    sudo mkdir $PATH_ROOTFS/sddisk
fi

if [ ! -d $PATH_ROOTFS/udisk ]; then
    sudo mkdir $PATH_ROOTFS/udisk
fi


if [ ! -c $PATH_ROOTFS/dev/null ]; then
    sudo mknod -m 666 $PATH_ROOTFS/dev/null c 1 3
fi

if [ ! -c $PATH_ROOTFS/dev/console ]; then
    sudo mknod -m 600 $PATH_ROOTFS/dev/console c 5 1
fi


sudo chmod -R 755  $PATH_ROOTFS
sudo chgrp -R root $PATH_ROOTFS
sudo chown -R root $PATH_ROOTFS


if [ ! -d $PATH_IMAGES ]; then
    mkdir $PATH_IMAGES
else
    if [ -f $PATH_IMAGES/$IMG_NAME ]; then
        rm $PATH_IMAGES/$IMG_NAME
    fi
fi

mkyaffs2image_for_NRM3358 $PATH_ROOTFS $PATH_IMAGES/$IMG_NAME

        
echo "make image root.bin done"

```


## UBIFS 制作工具

```
sudo apt-get install libacl1-dev
sudo apt-get install zlib1g-dev
sudo apt-get install liblzo2-dev
sudo apt-get install uuid-dev

git clone git://git.infradead.org/mtd-utils.git

make
sudo make install
```

```
mkfs.ubifs -F -v -r $PATH_ROOTFS -o $PATH_IMAGES/$IMGFS_NAME -m 4096 -e 253952 -c 2081
ubinize -o $PATH_IMAGES/$IMG_NAME -m 4096 -p 256KiB -s 4096 ubinize.cfg
```

mkfs.ubifs 选项的意义：
```
-m, --min-io-size=SIZE   minimum I/O unit size一般为页大小
-e, --leb-size=SIZE      logical erase block size(每块的页数-2)*页大小
-c, --max-leb-cnt=COUNT  maximum logical erase block count
-F, --space-fixup        file-system free space has to be fixed up on first mount
                         (requires kernel version 3.0 or greater)
```

ubinize 选项的意义：
```
-p, --peb-size=<bytes>       size of the physical eraseblock of the flash
                             this UBI image is created for in bytes,
                             kilobytes (KiB), or megabytes (MiB) 每块的页数*页大小
                             (mandatory parameter)
-m, --min-io-size=<bytes>    minimum input/output unit size of the flash
                             in bytes
-s, --sub-page-size=<bytes>  minimum input/output unit used for UBI
                             headers, e.g. sub-page size in case of NAND
                             flash (equivalent to the minimum input/output
                             unit size by default)

```


----
**文章来源：** 
>原创 zhxianbin@163.com

**修改记录：**
> 2015-08-22  首次发布

**参考资料：**
>[http://www.cnblogs.com/Charles-Zhang-Blog/p/3419301.html](http://www.cnblogs.com/Charles-Zhang-Blog/p/3419301.html)

>[http://blog.chinaunix.net/uid-26310563-id-3168454.html](http://blog.chinaunix.net/uid-26310563-id-3168454.html)

>[http://blog.chinaunix.net/uid-26310563-id-3168454.html](http://blog.chinaunix.net/uid-26310563-id-3168454.html)