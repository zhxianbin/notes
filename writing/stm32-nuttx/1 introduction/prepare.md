# nuttx 开发指南

## nuttx 开发环境配置

### 获取源码

nuttx 可以从以下地址下载：
> [http://sourceforge.net/projects/nuttx/files/](http://sourceforge.net/projects/nuttx/files/)

当前（2017.12.10）版本为 7.22

### 配置 nuttx
进入 nuttx-repo/nuttx
`cd tools`
`./configure.sh stm3210e-eval/nsh`
`cd ../`

### 交叉编译器

可以使用 buildroot 制作交叉编译器，也可以使用通用 GNU 工具链：

#### buildroot 制作

1 安装 GMP/MPFR/MPC/ZLIB
```
sudo apt-get install libgmp-dev
sudo apt-get install libmpfr-dev
sudo apt-get install libmpc-dev
sudo apt-get install zlib1g-dev
```

2 编译

进入 nuttx-repo/misc
```
cd buildroot
cp configs/cortexm3-eabi-defconfig-4.8.2 .config`
make menuconfig
make
```

#### 通用 GNU 工具链

下载地址：

### 编译 Nuttx
Nuttx 的编译与 Linux 类似：
[kconfig-frontends](http://ymorin.is-a-geek.org/projects/kconfig-frontends)
`make menuconfig`
`make`


## 源码分析


## 第一个应用程序 ---- 流水灯

1 在 nuttx-repo/apps 目录内新建一个目录 gowin（公司名称），用来存放项目代码；
2 修改 nuttx-repo/apps 目录内的 Kconfig、Makefile、Make.def：
- Kconfig 内加入：
```
menu "Gowin(Company name) Applications"
source "$APPSDIR/gowin/Kconfig"
endmenu
```

- Makefile 内，SUBDIRS 变量内增加 gowin，增加行
```
include gowin/Make.defs
```

- Make.def 无需修改

3 gowin 的目录结构与 example 类似，可以先将 example 内的 Kconfig、Make.def、Makefile 拷贝过来，然后修改；
4 在 gowin 目录内新建一个文件夹 led，存放流水灯代码；
5 修改 Kconfig，仿照原来的加入：
```
source "$APPSDIR/gowin/led/Kconfig"
```
