[TOC]
----

# cgdb 远程调试


## 环境

TARGET：TQ3358（192.168.1.30）
HOST：ubuntu-12.04 LTS（192.168.1.20）


## TARGET 端

通过nfs启动后，运行：
`gdbserver 192.168.1.20:2345 <program> ( gdbserver <host-ip>:<port> <program> )`


## HOST 端

在终端运行：
`cgdb -d arm-linux-gdb <program`
 
cgdb启动后，在GDB窗口运行：
`target remote 192.168.1.30:2345 ( target remote <target-ip>:<port> )`
    

----
**文章来源：** 
>原创 zhxianbin@163.com

**修改记录：**
> 2017-04-02  首次发布

**参考资料：**
> todo