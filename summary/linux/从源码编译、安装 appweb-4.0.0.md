[TOC]
----

# 从源码编译、安装 appweb-4.0.0

## 关于 appweb

http://www.appwebserver.org 对 appweb 的介绍：
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


## 编译、安装 appweb-4.0.0

appweb 提供3种编译方式：
>bit（Build It）工具
>make（windows系统的nmake）
>IDE，如Visual Studio 、XCode

其中，bit方式最灵活、可进行配置，推荐使用。由于 bit 包含在 Ejscript 中，所以还需要编译 Ejscript。故首先编译 ejscript 得到 bit，使用 bit 配置、编译、安装 appweb，具体步骤如下（以下假设 zlib、ejscript、appweb 的源码均位于 ~/work/ 目录）：
 
1. sudo apt-get install libapm-dev
 
2. 编译 zlib
./configure
make
 
3. make编译ejscript
make
编译结束后提示：You can now use Ejscript or use "bit" to customize and re-build Ejscript, via:
linux-x86-debug/bin/bit configure build
 
4. bit 重新编译ejscript
linux-x86-debug/bin/bit configure --release --with zlib=~/work/zlib-1.2.7/
linux-x86-debug/bin/bit
 
5. bit 配置、编译、安装 appweb-4.0.0
../ejs-2.0.0/linux-x86-release/bin/bit configure --release --with ejscript=~/work/ejs-2.0.0
../ejs-2.0.0/linux-x86-release/bin/bit
../ejs-2.0.0/linux-x86-release/bin/bit install

## 测试

`sudo appweb --config /etc/appweb/appweb.conf &`
在浏览器中输入 192.168.200.20（网卡IP地址），可以看到 appweb 页面，输入 192.168.200.20/test/test.html 可以看到 “Hello world”。


----
**文章来源：** 
>原创 zhxianbin@163.com

**修改记录：**
> 2017-04-02  首次发布

**参考资料：**
> todo