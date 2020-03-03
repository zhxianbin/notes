[TOC]
----

# SAMA5D4 Xplained Ultra 5 - �����ֲ


## ����

*TODO*


## libmodbus

��������վ���� busybox Դ�룬��ǰ���°汾�� v3.1.2��
[http://libmodbus.org/](http://libmodbus.org/)

```
./autogen.sh
CC=arm-none-linux-gnueabi-gcc ./configure --build=x86_64-linux --host=arm-linux --prefix=/home/me/projects/sama5d4x_xult/rootfs/opt/libmodbus
make
sudo make install
```


## SQLite

��������վ���� SQLite Դ�룬��ǰ���°汾�� 3.8.11.1��
[www.sqlite.org/](www.sqlite.org/)

```
CC=arm-none-linux-gnueabi-gcc ./configure --build=x86_64-linux --host=arm-linux --prefix=/home/me/projects/sama5d4x_xult/rootfs/opt/sqlite
make
sudo make install-strip
```


## appweb

��������վ���� appweb Դ�룬��ǰ���°汾�� v6.0.2��
[https://embedthis.com/index.html](https://embedthis.com/index.html)
���⣬Appweb �����á����뻹��Ҫʹ�� MakeMe��Pak

**1 ���� MakeMe**

���� MakeMe Դ��Ŀ¼
```
sudo apt-get install libssl-dev
make boot
```
�� build/linux-x64-release/bin ������ ~/tools/embedthis/makeme

**2 ���� Pak**

���� Pak Դ��Ŀ¼
```
~/tools/embedthis/makeme/bin/me configure --release
~/tools/embedthis/makeme/bin/me
```
�� build/linux-x64-release/bin ������ ~/tools/embedthis/pak

**3 ���� Expansive**

���� Expansive Դ��Ŀ¼
```
~/tools/embedthis/makeme/bin/me configure --release
~/tools/embedthis/makeme/bin/me
```
�� build/linux-x64-release/bin ������ ~/tools/embedthis/expansive

**4 ���밲װ Appweb**

```
~/tools/embedthis/makeme/bin/me configure --help

~/tools/embedthis/pak/bin/pak install appweb-ejscript
~/tools/embedthis/pak/bin/pak install sqlite

CC=arm-none-linux-gnueabi-gcc LD=arm-none-linux-gnueabi-ld ~/tools/embedthis/makeme/bin/me configure --release --with cgi --with dir --with ejscript --with esp --with http --with sqlite --platform linux-arm-release --with cgi --with dir --with ejscript --with esp --with http --with sqlite
~/tools/embedthis/makeme/bin/me
```
[https://embedthis.com/catalog/#/](https://embedthis.com/catalog/#/)

----
**������Դ��** 
>ԭ�� zhxianbin@163.com

**�޸ļ�¼��**
> 2015-08-22  �״η���

**�ο����ϣ�**
> todo