# union 与大小端模式

## 大端模式和小端模式 

- 大端模式(Big_endian)：字数据的高字节存储在低地址中，而字数据的低字节则存放在高地址中。

- 小端模式(Little_endian)：字数据的高字节存储在高地址中，而字数据的低字节则存放在低地址中。


## union 变量在大小端模式下的输出

```C
int main()
{
    union
    {
        int i;
        char a[2];
    }*p, u;
    
    p=&u;
    u.i = 0;
    
    p->a[0] = 0x12;
    p->a[1] = 0x34;
    printf("i = 0x%x\n", u.i);
}
```
 
输出：小端模式 —— 0x3412;大端模式 —— 0x1234。
解析：union型数据所占的空间等于其最大的成员所占的空间。对 union型的成员的存取都是相对于该联合体基地址的偏移量为 0 处开始，也就是联合体的访问不论对哪个变量的存取都是从 union的首地址位置开始。


## 使用union测试系统的存储模式

```C
int main()
{
    union
    {
        int i;
        char a[2];
    }*p, u;
    
    p=&u;
    u.i = 0x3412;
    
    if (0x12 == u.a[0])
    {
      printf("Little_endian\n");
    }
    else
    {
      printf("Big_endian\n");
    }
}
```

----
【 来源：原创 < zhxianbin@163.com > 】