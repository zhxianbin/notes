[TOC]
----

# 移植u-boot-2010.09到友善之臂mini2440(基于smdk2410)

## 新建开发板目录和文件

`board/samsung/`文件夹内，拷贝`smdk2410`文件夹，重命名为`mini2440`；修改`mini2440`文件夹内的文件名和`Makefile`，将`smdk2410`修改为`mini2440`；
`include/configs`文件夹内，拷贝`smdk2410.h`文件，重命名为`mini2440.h`；
打开源码根文件夹内的`boards.cfg`，拷贝`smdk2410`所在行（L.240），将`smdk2410`修改为`mini2440`。

编译测试：`make mini2440_config`，`make all`。成功！


## 修改include/configs/mini2440.h
将mini2440.h内 CONFIG_S3C2410 改为 CONFIG_S3C2440；CONFIG_SMDK2410 改为 CONFIG_MINI2440；将CS8900网卡改为DM9000。
编译测试：make distclean, make mini2440_config，make all；出现以下错误：
>include/asm/arch/s3c24x0_cpu.h:26:3: error: #error Please define the s3c24x0 cpu type

arch/arm/include/asm/arch-s3c24x0文件夹内，拷贝s3c2410.h文件，重命名为s3c2440.h；在s3c24x0_cpu.h内加入
```
#elif defined CONFIG_S3C2440
#include <asm/arch/s3c2440.h>
```

编译测试：`make distclean`, `make mini2440_config`，`make all`；出现以下错误：
>arch/arm/cpu/arm920t/s3c24x0/timer.c:187:3: error: #error "tbclk not configured"

在timer.c内加入
```
defined(CONFIG_MINI2440) || \
```
编译测试：`make distclean`, `make mini2440_config`，`make all`；出现以下错误：
>board/samsung/mini2440/mini2440.c: In function 'board_init':
board/samsung/mini2440/mini2440.c:91: error: 'struct s3c24x0_gpio' has no member named 'GPACON'
......

struct s3c24x0_gpio 在 arch/arm/include/asm/arch-s3c24x0/s3c24x0.h.内定义，加入：
```
#ifdef CONFIG_S3C2440
u32 GPACON;
......
#endif
```
编译测试，成功！

## 修改以上拷贝的文件
前面几步之后，虽然能编译通过，但文件内容都还是S3C2410的，有些可能与S3C2440不同，下面将逐个修改。
1. arch/arm/include/asm/arch-s3c24x0/s3c2440.h
将宏定义及函数返回类型中的 `S3C2410_*` 改为 `S3C2440_*`；`struct s3c2410_*` 定义在 `s3c24x0.h`文件内，改为 `struct s3c2440_*` 后也应在`s3c24x0.h`文件内加入定义。
```C
/* NAND FLASH (see S3C2440 manual chapter 6) */
struct s3c2440_nand {
    u32 NFCONF;
    u32 NFCONT;
    u32 NFCMD;
    u32 NFADDR;
    u32 NFDATA;
    u32 NFMECCD0;
    u32 NFMECCD1;
    u32 NFSECCD;
    u32 NFSTAT;
    u32 NFESTAT0;
    u32 NFESTAT1;
    u32 NFMECC0;
    u32 NFMECC1;
    u32 NFECC;
    u32 NFSBLK;
    u32 NFEBLK;
};

/* I/O PORT (see manual chapter 9) */
struct s3c24x0_gpio {
    ......
    #ifdef CONFIG_S3C2440
    u32 GPACON;
    u32 GPADAT;
    u32 res1[2];
    u32 GPBCON;
    u32 GPBDAT;
    u32 GPBUP;
    u32 res2;
    u32 GPCCON;
    u32 GPCDAT;
    u32 GPCUP;
    u32 res3;
    u32 GPDCON;
    u32 GPDDAT;
    u32 GPDUP;
    u32 res4;
    u32 GPECON;
    u32 GPEDAT;
    u32 GPEUP;
    u32 res5;
    u32 GPFCON;
    u32 GPFDAT;
    u32 GPFUP;
    u32 res6;
    u32 GPGCON;
    u32 GPGDAT;
    u32 GPGUP;
    u32 res7;
    u32 GPHCON;
    u32 GPHDAT;
    u32 GPHUP;
    u32 res8;
    u32 GPJCON;
    u32 GPJDAT;
    u32 GPJUP;
    u32 res9;
    
    u32 MISCCR;
    u32 DCLKCON;
    u32 EXTINT0;
    u32 EXTINT1;
    u32 EXTINT2;
    u32 EINTFLT0;
    u32 EINTFLT1;
    u32 EINTFLT2;
    u32 EINTFLT3;
    u32 EINTMASK;
    u32 EINTPEND;
    u32 GSTATUS0;
    u32 GSTATUS1;
    u32 GSTATUS2;
    u32 GSTATUS3;
    u32 GSTATUS4;
    u32 res10;
    u32 DSC0;
    u32 DSC1;
    u32 MSLCON;
    #endif
};

/* ADC (see manual chapter 16) */
struct s3c2440_adc {
    u32 ADCCON;
    u32 ADCTSC;
    u32 ADCDLY;
    u32 ADCDAT0;
    u32 ADCDAT1;
    u32 ADCUPDN;
};

/* SD INTERFACE (see S3C2440 manual chapter 19) */
struct s3c2440_sdi {
    u32 SDICON;
    u32 SDIPRE;
    u32 SDICARG;
    u32 SDICCON;
    u32 SDICSTA;
    u32 SDIRSP0;
    u32 SDIRSP1;
    u32 SDIRSP2;
    u32 SDIRSP3;
    u32 SDIDTIMER;
    u32 SDIBSIZE;
    u32 SDIDCON;
    u32 SDIDCNT;
    u32 SDIDSTA;
    u32 SDIFSTA;
    u32 SDIIMSK;
    #ifdef __BIG_ENDIAN
    u8 res[3];
    u8 SDIDAT;
    #else
    u8 SDIDAT;
    u8 res[3];
    #endif
};
```
编译测试，成功！

2. board/samsung/mini2440/mini2440.c
```
#elif FCLK_SPEED==1 /* Fout = 202.8MHz */
#define M_MDIV 0xA1
#define M_PDIV 0x3
#define M_SDIV 0x1
#endif
```
改为
```
#elif FCLK_SPEED==1 /* Fout = 400MHz */
#define M_MDIV 0x5c
#define M_PDIV 0x1
#define M_SDIV 0x1
#endif
```

```
#elif USB_CLOCK==1
#define U_M_MDIV 0x48
#define U_M_PDIV 0x3
#define U_M_SDIV 0x2
#endif
```
改为
```
#elif USB_CLOCK==1 /* Fout = 48MHz */
#define U_M_MDIV 0x38
#define U_M_PDIV 0x2
#define U_M_SDIV 0x2
#endif
```
将 board_init() 函数中
```
/* arch number of SMDK2410-Board */
gd->bd->bi_arch_number = MACH_TYPE_SMDK2410;
```
改为
```
/* arch number of MINI2440-Board */
gd->bd->bi_arch_number = MACH_TYPE_MINI2440;
```
MACH_TYPE_MINI2440 定义在 arch/arm/include/asm/mach-types.h 内。

## 根据启动流程修改相关文件
1. arch/arm/cpu/arm920t/start.S
注释掉以下2行：
>bl coloured_LED_init
bl red_LED_on

```
# if defined(CONFIG_S3C2410)
ldr r1, =0x3ff
ldr r0, =INTSUBMSK
str r1, [r0]
# endif
```

后面，添加：

```
# if defined(CONFIG_S3C2440)
ldr r1, =0x3fff
ldr r0, =INTSUBMSK
str r1, [r0]
# endif
```

```
/* FCLK:HCLK:PCLK = 1:2:4 */
/* default FCLK is 120 MHz ! */
ldr r0, =CLKDIVN
mov r1, #3
str r1, [r0]
```

改为

```
/* FCLK:HCLK:PCLK = 1:4:8 */
/* default FCLK is 400 MHz ! */
ldr r0, =CLKDIVN
mov r1, #5
str r1, [r0]
```
3. 支持从NandFlash启动
修改：
```
#ifndef CONFIG_SKIP_RELOCATE_UBOOT
relocate: /* relocate U-Boot to RAM */
adr r0, _start /* r0 <- current position of code */
ldr r1, _TEXT_BASE /* test if we run from flash or RAM */
cmp r0, r1 /* don't reloc during debug */
beq stack_setup

ldr r2, _armboot_start
ldr r3, _bss_start
sub r2, r3, r2 /* r2 <- size of armboot */
add r2, r0, r2 /* r2 <- source end address */

copy_loop:
ldmia r0!, {r3-r10} /* copy from source address [r0] */
stmia r1!, {r3-r10} /* copy to target address [r1] */
cmp r0, r2 /* until source end addreee [r2] */
ble copy_loop
#endif /* CONFIG_SKIP_RELOCATE_UBOOT */
```
替换为：
```
/************** 将 NAND/NOR Flash 中的代码拷贝至 RAM ***********************/
#ifndef CONFIG_SKIP_RELOCATE_UBOOT
relocate: /* relocate U-Boot to RAM */ 
adr r0, _start /* r0 <- current position of code */ 
ldr r1, _TEXT_BASE /* test if we run from flash or RAM */ 
cmp r0, r1 /* don't reloc during debug */ 
beq stack_setup 

ldr r2, _armboot_start 
ldr r3, _bss_start 
sub r2, r3, r2 /* r2 <- size of armboot(r3 - r2) */

bl CopyCode2Ram /* r0: source, r1: dest, r2: size */
#endif
/************** 将 NAND/NOR Flash 中的代码拷贝至 RAM ***********************/
```
同时在board/samsung/mini2440目录添加文件 boot_init.c，修改Makefile，boot_init.c文件内容如下：
```
#include <common.h>
#include <asm/arch/s3c24x0_cpu.h>

#define GSTATUS1 (*(volatile unsigned int *)0x560000B0)
#define BUSY 1

/* 供外部调用的函数 */
void nand_init_ll(void);
void nand_read_ll(unsigned char *buf, unsigned long start_addr, int size);

/* NAND Flash的操作函数 */
static void nand_reset(void);
static void wait_idle(void);
static void nand_select_chip(void);
static void nand_deselect_chip(void);
static void write_cmd(int cmd);
static void write_addr(unsigned int addr);
static unsigned char read_data(void);


/* 在第一次使用NAND Flash前，复位一下NAND Flash */
static void nand_reset(void)
{
nand_select_chip();
write_cmd(0xff); // 复位命令
wait_idle();
nand_deselect_chip();
}

/* 等待NAND Flash就绪 */
static void wait_idle(void)
{
int i;
struct s3c2440_nand * s3c2440nand = (struct s3c2440_nand *)0x4e000000;
volatile unsigned char *p = (volatile unsigned char *)&s3c2440nand->NFSTAT;

while(!(*p & BUSY))
for(i=0; i<10; i++);
}

/* 发出片选信号 */
static void nand_select_chip(void)
{
int i;
struct s3c2440_nand * s3c2440nand = (struct s3c2440_nand *)0x4e000000;

s3c2440nand->NFCONT &= ~(1<<1);
for(i=0; i<10; i++); 
}

/* 取消片选信号 */
static void nand_deselect_chip(void)
{
struct s3c2440_nand * s3c2440nand = (struct s3c2440_nand *)0x4e000000;

s3c2440nand->NFCONT |= (1<<1);
}

/* 发出命令 */
static void write_cmd(int cmd)
{
struct s3c2440_nand * s3c2440nand = (struct s3c2440_nand *)0x4e000000;

volatile unsigned char *p = (volatile unsigned char *)&s3c2440nand->NFCMD;
*p = cmd;
}

/* 发出地址 */
static void write_addr(unsigned int addr)
{
int i;
struct s3c2440_nand * s3c2440nand = (struct s3c2440_nand *)0x4e000000;
volatile unsigned char *p = (volatile unsigned char *)&s3c2440nand->NFADDR;

*p = addr & 0xff;
for(i=0; i<10; i++);
*p = (addr >> 9) & 0xff;
for(i=0; i<10; i++);
*p = (addr >> 17) & 0xff;
for(i=0; i<10; i++);
*p = (addr >> 25) & 0xff;
for(i=0; i<10; i++);
}

/* 读取数据 */
static unsigned char read_data(void)
{
struct s3c2440_nand * s3c2440nand = (struct s3c2440_nand *)0x4e000000;
volatile unsigned char *p = (volatile unsigned char *)&s3c2440nand->NFDATA;
return *p;
}

/* 初始化NAND Flash */
void nand_init_ll(void)
{
struct s3c2440_nand * s3c2440nand = (struct s3c2440_nand *)0x4e000000;

#define TACLS 0
#define TWRPH0 3
#define TWRPH1 0

/* 设置时序 */
s3c2440nand->NFCONF = (TACLS<<12)|(TWRPH0<<8)|(TWRPH1<<4);
/* 使能NAND Flash控制器, 初始化ECC, 禁止片选 */
s3c2440nand->NFCONT = (1<<4)|(1<<1)|(1<<0);

/* 复位NAND Flash */
nand_reset();
}


#define NAND_SECTOR_SIZE 512
#define NAND_BLOCK_MASK (NAND_SECTOR_SIZE - 1)

/* 读函数 */
void nand_read_ll(unsigned char *buf, unsigned long start_addr, int size)
{
int i, j;

if ((start_addr & NAND_BLOCK_MASK) || (size & NAND_BLOCK_MASK)) 
{
return ; /* 地址或长度不对齐 */
}

/* 选中芯片 */
nand_select_chip();

for( i=start_addr; i < (start_addr + size); ) 
{
/* 发出READ0命令 */
write_cmd(0);

/* Write Address */
write_addr(i);
wait_idle();

for(j=0; j < NAND_SECTOR_SIZE; j++, i++) 
{
*buf = read_data();
buf++;
}
}

/* 取消片选信号 */
nand_deselect_chip();

return ;
}

int bBootFrmNORFlash(void)
{
volatile unsigned int *pdw = (volatile unsigned int *)0;
unsigned int dwVal;

/*
* 无论是从NOR Flash还是从NAND Flash启动，
* 地址0处为指令"b Reset", 机器码为0xEA00000B，
* 对于从NAND Flash启动的情况，其开始4KB的代码会复制到CPU内部4K内存中，
* 对于从NOR Flash启动的情况，NOR Flash的开始地址即为0。
* 对于NOR Flash，必须通过一定的命令序列才能写数据，
* 所以可以根据这点差别来分辨是从NAND Flash还是NOR Flash启动:
* 向地址0写入一个数据，然后读出来，如果没有改变的话就是NOR Flash
*/

dwVal = *pdw; 
*pdw = 0x12345678;
if (*pdw != 0x12345678)
{
return 1;
}
else
{
*pdw = dwVal;
return 0;
}
}

int CopyCode2Ram(unsigned long start_addr, unsigned char *buf, int size)
{
unsigned int *pdwDest;
unsigned int *pdwSrc;
int i;

if (bBootFrmNORFlash())
{
pdwDest = (unsigned int *)buf;
pdwSrc = (unsigned int *)start_addr;
/* 从 NOR Flash启动 */
for (i = 0; i < size / 4; i++)
{
pdwDest[i] = pdwSrc[i];
}
return 0;
}
else
{
/* 初始化NAND Flash */
nand_init_ll();
/* 从 NAND Flash启动 */
nand_read_ll(buf, start_addr, (size + NAND_BLOCK_MASK)&~(NAND_BLOCK_MASK));
return 0;
}
}

static inline void delay (unsigned long loops)
{
__asm__ volatile ("1:\n"
"subs %0, %1, #1\n"
"bne 1b":"=r" (loops):"0" (loops));
}
```

修改 arch/arm/cpu/arm920t/u-boot.lds的.text段
.text :
{
arch/arm/cpu/arm920t/start.o (.text)
board/samsung/mini2440/lowlevel_init.o (.text)
board/samsung/mini2440/boot_init.o (.text)
*(.text)
}


----
**文章来源：** 
>原创 zhxianbin@163.com

**修改记录：**
> 2017-04-02  首次发布

**参考资料：**
> todo