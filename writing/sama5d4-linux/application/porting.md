[TOC]
----

# SAMA5D4 Xplained Ultra 5 - 软件移植


## 概述

*TODO*


## libmodbus

从以下网站下载 busybox 源码，当前最新版本是 v3.1.2：
[http://libmodbus.org/](http://libmodbus.org/)

```
./autogen.sh
CC=arm-none-linux-gnueabi-gcc ./configure --build=x86_64-linux --host=arm-linux --prefix=/home/me/projects/sama5d4x_xult/rootfs/opt/libmodbus
make
sudo make install
```


## SQLite

从以下网站下载 SQLite 源码，当前最新版本是 3.8.11.1：
[www.sqlite.org/](www.sqlite.org/)

```
CC=arm-none-linux-gnueabi-gcc ./configure --build=x86_64-linux --host=arm-linux --prefix=/home/me/projects/sama5d4x_xult/rootfs/opt/sqlite
make
sudo make install-strip
```


## appweb

从以下网站下载 appweb 源码，当前最新版本是 v6.0.2：
[https://embedthis.com/index.html](https://embedthis.com/index.html)
另外，Appweb 的配置、编译还需要使用 MakeMe、Pak

**1 编译 MakeMe**

进入 MakeMe 源码目录
```
sudo apt-get install libssl-dev
make boot
```
将 build/linux-x64-release/bin 拷贝到 ~/tools/embedthis/makeme

**2 编译 Pak**

进入 Pak 源码目录
```
~/tools/embedthis/makeme/bin/me configure --release
~/tools/embedthis/makeme/bin/me
```
将 build/linux-x64-release/bin 拷贝到 ~/tools/embedthis/pak

**3 编译 Expansive**

进入 Expansive 源码目录
```
~/tools/embedthis/makeme/bin/me configure --release
~/tools/embedthis/makeme/bin/me
```
将 build/linux-x64-release/bin 拷贝到 ~/tools/embedthis/expansive

**4 编译安装 Appweb**

```
~/tools/embedthis/makeme/bin/me configure --help

~/tools/embedthis/pak/bin/pak install appweb-ejscript
~/tools/embedthis/pak/bin/pak install sqlite

CC=arm-none-linux-gnueabi-gcc LD=arm-none-linux-gnueabi-ld ~/tools/embedthis/makeme/bin/me configure --release --with cgi --with dir --with ejscript --with esp --with http --with sqlite --platform linux-arm-release --with cgi --with dir --with ejscript --with esp --with http --with sqlite
~/tools/embedthis/makeme/bin/me
```
[https://embedthis.com/catalog/#/](https://embedthis.com/catalog/#/)

----
**文章来源：** 
>原创 zhxianbin@163.com

**修改记录：**
> 2015-08-22  首次发布

**参考资料：**
> todo