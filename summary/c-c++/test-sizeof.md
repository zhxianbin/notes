[TOC]
----

# 基本数据类型的 sizeof 测试


```C
# include < iostream >

using namespace std;

int main()
{
　　cout << "sizeof(char) = " << sizeof ( char ) << endl;
　　cout << "sizeof(unsigned char) = " << sizeof ( unsigned char ) << endl;
　　cout << "sizeof(short int) = " << sizeof ( short int ) << endl;
　　cout << "sizeof(unsigned short int) = " << sizeof ( unsigned short int ) << endl;
　　cout << "sizeof(int) = " << sizeof ( int ) << endl;
　　cout << "sizeof(unsigned int) = " << sizeof ( unsigned int ) << endl;
　　cout << "sizeof(long int) = " << sizeof ( long int ) << endl;
　　cout << "sizeof(unsigned long int) = " << sizeof ( unsigned long int ) << endl;
　　cout << "sizeof(float) = " << sizeof ( float ) << endl;
　　cout << "sizeof(double) = " << sizeof ( double ) << endl;
　　cout << "sizeof(long double) = " << sizeof ( long double ) << endl;

    return 0;
}
```


----
**文章来源：** 
> 原创 zhxianbin@163.com

**修改记录：**
> 2017-04-02  首次发布

**参考资料：**
> todo