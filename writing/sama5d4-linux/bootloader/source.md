# 源码分析


从 `arch/arm/cpu/u-boot.lds` 的 `ENTRY(_start)` 可以看到 u-boot 的入口是 _start

1. _start(arch/arm/lib/vectors.S)

- 跳转到 reset。

2. reset(arch/arm/cpu/armv7/start.S)

- save_boot_params /* Allow the board to save important registers */
- disble interrupt
- cpu_init_cp15
- cpu_init_crit
- 跳转到 _main；

3. _main（arch/arm/lib/crt0.S）

- TODO
- 跳转到 relocate_code
- TODO

4. relocate_code(arch/arm/lib/relocate.S)

- TODO

5. u-boot-spl 从 nand flash 拷贝 u-boot 至 RAM 运行，需要以下几个参数：
- 从 nand flash 的什么位置拷贝；
- 拷贝至 RAM 的什么位置
- 拷贝的大小