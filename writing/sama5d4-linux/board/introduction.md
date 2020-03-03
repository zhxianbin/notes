# SAMA5D4 Xplained Ultra


## AT91Bootstrap

```
git clone git://github.com/linux4sam/at91bootstrap.git
make mrproper
make sama5d4_xplainednf_uboot_secure_defconfig
make menuconfig
make CROSS_COMPILE=arm-none-linux-gnueabi-
```
sama5d4_xplainednf_uboot_secure_defconfig
sama5d4_xplainedsd_uboot_secure_defconfig


## U-Boot

```
git clone git://github.com/linux4sam/u-boot-at91.git
make sama5d4_xplained_nandflash_defconfig
make
```

## Linux

```
$ git clone git://github.com/linux4sam/linux-at91.git
```


## 启动分析

复位后，SAMA5D4 Series 系列 CPU 内 128-Kbyte ROM 被映射到 0x0 地址


## 烧写

1. 短接 JP7（BOOT_DIS）；
2. USB 接到 J11（A5-USB-A）；
3. 断开 JP7;
4. 执行 .bat。

----
**文章来源：** 
>原创 zhxianbin@163.com

**修改记录：**
> 2015-08-22  首次发布

**参考资料：**
> todo