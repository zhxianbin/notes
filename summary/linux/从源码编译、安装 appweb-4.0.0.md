[TOC]
----

# ��Դ����롢��װ appweb-4.0.0

## ���� appweb

http://www.appwebserver.org �� appweb �Ľ��ܣ�
>Appweb is a standards-based embedded HTTP server that has a wealth of features including:
Full HTTP/1.1 web server
Multi-threaded, event-driven core: fastest performance in its class
Dynamically loadable modules
Server-side JavaScript web framework
In-memory PHP module
In-process CGI as well as traditional CGI
Apache compatible configuration and logging
Basic and Digest Authentication
Secure Socket Layer (SSL/TLS)
Session state data management
HTTP Client program and library
ROMable web pages and configuration files
Cross-platform and portable
Embeddable in applications and devices (supports XIP)
Modular source code and documentation provided


## ���롢��װ appweb-4.0.0

appweb �ṩ3�ֱ��뷽ʽ��
>bit��Build It������
>make��windowsϵͳ��nmake��
>IDE����Visual Studio ��XCode

���У�bit��ʽ�����ɽ������ã��Ƽ�ʹ�á����� bit ������ Ejscript �У����Ի���Ҫ���� Ejscript�������ȱ��� ejscript �õ� bit��ʹ�� bit ���á����롢��װ appweb�����岽�����£����¼��� zlib��ejscript��appweb ��Դ���λ�� ~/work/ Ŀ¼����
 
1. sudo apt-get install libapm-dev
 
2. ���� zlib
./configure
make
 
3. make����ejscript
make
�����������ʾ��You can now use Ejscript or use "bit" to customize and re-build Ejscript, via:
linux-x86-debug/bin/bit configure build
 
4. bit ���±���ejscript
linux-x86-debug/bin/bit configure --release --with zlib=~/work/zlib-1.2.7/
linux-x86-debug/bin/bit
 
5. bit ���á����롢��װ appweb-4.0.0
../ejs-2.0.0/linux-x86-release/bin/bit configure --release --with ejscript=~/work/ejs-2.0.0
../ejs-2.0.0/linux-x86-release/bin/bit
../ejs-2.0.0/linux-x86-release/bin/bit install

## ����

`sudo appweb --config /etc/appweb/appweb.conf &`
������������� 192.168.200.20������IP��ַ�������Կ��� appweb ҳ�棬���� 192.168.200.20/test/test.html ���Կ��� ��Hello world����


----
**������Դ��** 
>ԭ�� zhxianbin@163.com

**�޸ļ�¼��**
> 2017-04-02  �״η���

**�ο����ϣ�**
> todo