[TOC]
----

# cgdb Զ�̵���


## ����

TARGET��TQ3358��192.168.1.30��
HOST��ubuntu-12.04 LTS��192.168.1.20��


## TARGET ��

ͨ��nfs���������У�
`gdbserver 192.168.1.20:2345 <program> ( gdbserver <host-ip>:<port> <program> )`


## HOST ��

���ն����У�
`cgdb -d arm-linux-gdb <program`
 
cgdb��������GDB�������У�
`target remote 192.168.1.30:2345 ( target remote <target-ip>:<port> )`
    

----
**������Դ��** 
>ԭ�� zhxianbin@163.com

**�޸ļ�¼��**
> 2017-04-02  �״η���

**�ο����ϣ�**
> todo