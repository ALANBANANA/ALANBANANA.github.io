# C语言笔记

## 一.第一个C语言程序

### 1.1 第一个程序的剖析

```C
// 这是主函数
int main() //表示一个主函数 (int表示整数型，main为函数名称)
{
    //主函数返回值 ————>注释：标注代码用途和思路，不会被编译
    printf('hello world\n')
    return 0; //表示函数的返回值
} // --->函数做的处理要在花括号里
```

### 1.2 练习

```c
int add(int a, int b)
{
    return a + b;
}
```

* 当前之下，add函数并不能进行调用， 所以每一个函数必须要先有主函数[^mian]进行

以下为正确的实例，编译器会往下进行阅读

```c
#include <stdio.h>
int add(int a; int b)
{
    return a + b
}
int main()
{
    int rusult;
    result = add(2, 3);
    printf("%d", result);
    return 0
}
```

倘若add函数在main函数，那么这个程序将无法照常进行将会报错

以下是主函数必须要有的特征

* 主函数会被自动调用
* 返回值给调用的程序
* 主函数返回值必须是int，正常进行的则为0

## 二.变量

### 2.1 赋值运算符

__“ = ”__ 在编程上与数学的等号具有很大的差别，是指将“=”左边的数用一些__右边数字__进行赋值

**“ == ”**在编程上则与数学上的等号相同，即为等值

### 2.2 标识符

变量需要被先声明在进行使用，如上面的__add__，以及变量__a__,__b__

#### 2.2.1 标识符种类分别 

1. 变量 __a__,__b__
2. 函数 __add()__
3. 其他实体

#### 2.2.2 标识符命名规则

1. 标识符必须可以用小写字母、大写字母、数字和下划线命名
2. 标识符第一个字符必须是字母或者下划线，不可以是数字

#### 2.2.4 关键词

不可以作为标识符进行使用

#### 2.2.5 常量

1. 数字：1，2，3，4
2. 字符串：“Hello World”

#### 2.2.6 **printf**函数

形如`printf()` ----->为print 和format 的交和，用于输出指令到控制台

**printf**的公式：`printf("占位符1 占位符2 占位符3", 替换1, 替换2, 替换3)”会将“替换1”换到"占位符1)`,依次类推下去

#### 2.2.7 __include__命令

__“# include <stdio.h>“__引入头文件，其中包含了关于__"printf"__的定义

## 三.数据类型

### 3.1 整数类型

|            整数类型             |             数据表示             |
| :-----------------------------: | :------------------------------: |
|    字符串(关键字：__char__)     | 用于表示一个很小的整数，范围[-2] |
|    短整型(关键字：**short**)    |    用于表示一个不怎么大的整数    |
|      整型(关键字：__int__)      |    生活中一般的整数都可以表示    |
|    长整型(关键字：__long__)     |      用于表示一个较大的整数      |
| 加长整形(关键字：__long long__) |     用于表示一个非常大的整数     |

如此多整数的类型的原因：1. 占用内存大小不一样 2.表示数据范围不一样

高级别的数据类型范围不可以低于低级别的数据类型范围：__char__(1)<__short__(2)<int(4)<__long__(4)<__long long__(8)，用`sizeof()`函数，其中int和short的相同，说明可以一致但不可以小于，占用字节越多，数据也越大

### 3.2 整型数据的具体范围

1. char：1*8位，-2^7~2^7-1
2. short：2*8位，-2^15~2^15-1
3. int：4*8位，-2^31~2^31-1
4. long：4*8位，-2^31~-2^31-1
5. long long：8*8位，-2^63~2^63-1

类似不对应8，16，32，32，64是因为在最前面一位为数值的符号若是想不让最前面为符号位，则需要使用`unsigned()`,当即上面序号整数类型对应的__负数__将会失去，只代表__正数__，此外2头上的·次方将会变为8，16，32，32，64

### 3.3 浮点数据类型(float)

以下为例子

```C
#include <stdio.h>
int main()
{
    float a = 1.234567;
    float b = 0.000001;
    float c = 365.12345;
    printf("%f\n", a); // 百分号中的d前面是对应整数类型的
    printf("%f\n", b); // f则是对应浮点类型的
    printf("%f\n", c); // 而类似365.12345变为365.123444
    return 0;
}
```

由365.123444所以浮点数并不可以表示无限的精确，会有误差，__float类型至少能表示有效的6位数字，且可以表示至10^-37到10^37__

### 3.4 双精度浮点型(double)

```c
#include <stdio.h>
int main()
{
    double a = 1.234567;
    double b = 0.000001;
    double c = 365.12345;
    printf("%f\n", a); // 百分号中的d前面是对应整数类型的
    printf("%f\n", b); // f则是对应浮点类型的
    printf("%f\n", c); // 而类似365.12345变为365.123444
    return 0;
}
```

double也是有自己的精度范围的，即超出了则精度消失

__浮点类型，范围越大，精度越高，所占字节也就越大__

### 3.5 变量和常量

- 标识符：1.  自己命名的标识   2. 表示变量、函数或其他实体的名称    3. 必须声明和定义
- 关键词：1. C语言标准规范词汇   2. 有特殊意义和用途   3. 可以直接在程序使用

__声明变量公式__:__[数据类型 + 标识符名 + 分号]__---------->声明一个变量

```C
#include <stdio.h>
int main()
{
    int a; // 声明变量的具体操作，假如和下面式子对调则代码不可正确运行
    printf("%d\n", a);  // 使用变量一定先声明
    return a
}
```

#### 3.5.1 变量标识符的命名

1. 只能有大小写英文字母，数字或者下划线组成(Alan_banana)
2. 标识符不可以以数字开头(123a)
3. 标识符不可以是已有关键词(int str)

#### 3.5.2 变量处理

##### 变量声明后立即初始化

```c
#include <stdio.h>
int main()
{
    int a = 100;  // 声明后立即初始化————————>变量声明初始化
    printf("%d\n", a);
    return 0;
}
```

##### 变量先声明再变量赋值

```c
#include <stdio.h>
int main()
{
    int a;  // 并无直接初始化——————————>变量声明
    a = 100;  // 变量赋值
    printf("%d\n". a);  // %d %n %c %s %f……为占位符
    return 0;
}
```

**总结: 变量可以多次往脚本下面赋值，但不可以多次初始化**

#### 3.5.3 常量

##### 字面常量

即已经写死无法改变的常量例如：“100”， “Hello world”--->**字符串**，'h','e'--->**字符**

- 字面常量无需要进行声明， 编译器可以判断其类型
- 数字型会根据长度自己判断

##### 符号常量

> #define PRICE  3

在函数即为庞大时，使用符号常量有助于全体程序使用，使用符号修改可以方便进行修改

### 3.6 字符常量以及字符变量

#### 3.6.1 字符常量

Helloworld中的每一个字均由一个字符组成——>H, e, l, l, o, w, o, r, l, 均为一个字符

所以Helloword实际上为字符串

__字符常量是由单引号包括的__

```c
// 正确编写方式
#include <stdio.h>
int main()
{
    printf("%c%c%c%c%c%c%c%c%c%c", 
           'H', 'e', 'l', 'l', 'o', 'W', 'o', 'r', 'l', 'd');  // '':字符， "" 字符串
    return 0
}
```

__在C和CPP两个编译器之中对于字符串的位节大小是不相同的，C：4，CPP：1__

#### 3.6.2 字符变量

__字符变量在C语言当中一般用char来表示__

```c
#include <stdio.h>
int main()
{
    char c = 'A';
    printf("sizeof char = %d\n", sizeof(char));  //-------->只占用一个字节大小
    printf("sizeof c = %d\n", sizeof(c));  //-------->只占用一个字节大小
    return 0;
}
```

__整数与字符占位符区别__

```c
#include <stdio.h>
int main()
{
    printf("%d %d %d %d %d", 'a', 'b', 'c', 'd', 'e');
    return 0;
}  // 输出为一个连续的数字，即字符和数值有一一对应的关系
```

__字符类型仅需要一个字节大小__

| 进制字母 | 代表进制     |
| -------- | ------------ |
| DCT      | 十进制       |
| OCT      | 八进制       |
| HEX      | 十六进制     |
| CHAR     | 数值对应字符 |

所以字符类型就是整型类型：字符类型只占用一个字节

```c
#include <stdio.h>
int main()
{
    char c1 = 'a';
    char c2 = '\n';  //-------> \n:换行符
    char c3 = '1';
    printf("c1=%c c2=%c c3=%c", c1, c2, c3);
    return 0;
}
```

例题：利用ASCII将大写A赋值给一个名为letter的变量，并将大写A打印出来

```c
# include <stdio.h>
int main()
{
    char letter = 'A';
    letter = letter + 32;
    printf("letter = %c", letter);
    return 0;
}
```

##### 字符串所占用的大小

“HelloWorld”实际上为10个字符占用10节，可打印出来为11节，即末尾有一个0代表字符串的结束，“HelloWorld”中间加入0，如“Hello0World”却照常输入，所以0算是正常输出的字句

```c
#include <stdio.h>
int main()
{
	printf("sizeof Helloworld = %d\n", sizeof("Helloworld"));  // sizeof Helloworld = 11 > H(1)e(2)l(3)l(4)o(5)w(6)o(7)r(8)l(9)d(10)0(11)
	return 0;
}
```



#### 3.6.3 转义字符

```c
#include <stdio.h>
int main()
{
    printf("Hello\0World");
    return 0;
}  // ------>这时候只打印Hello这个字符，即word被截断
```

所以"\\"为转义字符------反斜杠使用八进制来进行打印

八进制打印hello

```c
#include <stdio.h>
int main()
{
	printf("\110\145\154\154\157");  // 八进制
	return 0;
}
```

##### 一般的转义字符

| ASII二进制表示       | 八进制表示 | 十进制 |
| -------------------- | ---------- | ------ |
| \12,以及\n都表示换行 | \12        | \10    |
| \a表示报警           | \7         | \7     |
| \b表示退格           | \10        | \8     |
| \f表示换页           | \14        | \12    |
| \r表示回车           | \15        | \13    |
| \t表示水平制表       | \11        | \9     |
| \v表示垂直制表       | \13        | \11    |

__上述没办法在键盘上直接表示为不可见字符__:用斜杠加数字表示或者斜杠加注记字母表示

ASCII的0~~31之间的为不可见字符



## 四.内置函数和占位符

### 4.1 printf函数

> printf("占位符1， 占位符2"， 替换1， 替换2)

1. printf是一个变参函数
2. printf是一个参数字符串
3. printf是一个参数需要输出的内容
4. printf的第二及后续参数将依次替换占位符
5. 占位符的类型和数量需要与后续参数一一对应

例子体现上述五条例子

```c
#include <stdio.h>
int main()
{
	int a = 100;
	float b = 3.14;
	char c = 'a';
	printf("a = %d b = %f c = %c", a, b, c);
	return 0;
}
```

**类型提升**：printf是一个可变参数函数，将参数传入函数的可变参数中，变量会发生自动类型提升

在printf函数中的类型提升如以下表格

|      数据类型      |   提升的数据类型   | 占位符 |
| :----------------: | :----------------: | :----: |
|        char        |        int         |   %d   |
|       short        |        int         |   %d   |
|        int         |        int         |   %d   |
|        long        |        long        |  %ld   |
|     long long      |     long long      |  %lld  |
|   unsigned char    |   unsigned char    |   %u   |
|   unsigned short   |   unsigned short   |   %u   |
|    unsigned int    |    unsigned int    |   %u   |
|   unsigned long    |   unsigned long    |  %lu   |
| unsigned long long | unsigned long long |  %llu  |

### 4.2 占位符转换规范

|  占位符例子  |  %   |        -+0#        |              12              |                   .4                   |                      l                       |              d              |
| :----------: | :--: | :----------------: | :--------------------------: | :------------------------------------: | :------------------------------------------: | :-------------------------: |
| 字符代表意思 |      | 零个或多个标志字符 | 可选十进制表示的最小字段宽度 | 一个可选表示精度范围后面跟着十进制整数 | 可选长度指示符，可用：h \hh \ l \ ll \ z表示 | 单个字符的转换操作：d、f、c |

**转换操作及转换方式**(满足ASCII码字符和数字转化)

| 转换操作 |                转换方式                 |
| :------: | :-------------------------------------: |
|    c     |               字符串类型                |
|    d     |                整型类型                 |
|    e     | 双精度浮点类型，e计数法表示：科学计数法 |
|    E     | 双精度浮点类型，e计数法表示：科学计数法 |
|    f     |              双精度浮点法               |
|    a     |             十六进制浮点值              |
|    o     |            无符号八进制类型             |
|    s     |                 字符串                  |
|    u     |               无符号整型                |
|    x     |           无符号十六进制整型            |
|    X     |           无符号十六进制整型            |

**长度指示符的操作**

| 长度指示符 | 转换操作   | 二进制字节长度n            |
| ---------- | ---------- | -------------------------- |
| l          | d或i       | sizeof(long)               |
| ll         | d或i       | sizeof(long long)          |
| l          | u或o或x或X | sizeof(unsigned long)      |
| ll         | u或o或x或X | sizeof(unsigned long long) |
| h          | d或i       | sizeof(short)              |
| hh         | d或i       | sizeof(char)               |
| h          | u或o或x或X | sizeof(unsigned short)     |
| hh         | u或o或x或X | sizeof(unsigned char)      |

**精度范围**

整数型的转换，精度可以控制最小位数(往数字位数大的补位)

浮点类型的转换操作，精度可以控制小数点后位数(往小数点右侧去补位)

**最小数字位数**:根据数字的长度，假如要四位，但实际两位，则在前面插入两个空格

**标志字符0-+#**：

1. 0：使用0而非空格填充字符
2. +：给数据上符号：负数为负，正数为正
3. -：给数据左右对齐，按数字位数来说，没有则右对齐，有则左对齐
4. #：八进制数据添加0，十六进制数据添加0X

```c
#include <stdio.h>
int main()
{
	int n = 1234;
	printf("%6d\n", n);  // 标志0：数字位数为6
	printf("%06d\n", n);//         将你前面选的数字位数用6来表示
	printf("%6d%6d\n", 1, 2);  //标志-： 右对齐
	printf("%-6d%-6d\n", 1, 2);  //      左对齐
	printf("%+6d\n", n);  //标志+让内容产生符号：正数为加，负数为负
	printf("%+06d\n", n);
	printf("%#o\n", n);  // 标志#：让八进制八进制结果加上0
	printf("%#X\n", n);  //        十六进制结果加上0X
	return 0;
}
```

### 4.3 scanf函数( ：说白了类似iPython里面的input(VS无法使用scanf函数)

加入如下字符串

printf函数->二进制数据->转换规范->字符

scanf->键盘输入字符->转换规范->二进制

```c
#include <stdio.h>
int main()
{
	char c;
	short s;
	int n;
	long l;
	float f;
	double df;
	scanf("%hhd %hd %d %ld %f %lf", &c, &s, &n, &l, &f, &df);
	printf("%d %d %d %d %f %f\n", c, s, n, l, f, df);
	return 0;
}
```

**scanf**函数使用公式：

```c
scanf("%hhd %hd %d %ld %f %lf", &c, &s, &n, &l, &f, &df)  // 第一个参数内容是“”字符串，里面符合转换规范，输入要符合第一个字符串里面的参数如输入1 2 3 4 5.6 7.8，分割形式也要相同，匹配失败会报错，转换的参数是数据的存放位置
```

1. scanf是一个变参函数
2. scanf的第一个参数字符串
3. scanf的第一个参数内容为匹配字符以及转换规范
4. scanf的后续参数是数据存放位置
5. 转换规范的写法与数量，需要与后续参数一一对应

![6731ed820b24e1de1ec5948b477ecd1](C:\Users\DELL\Documents\WeChat Files\wxid_r87uet4wdjgp12\FileStorage\Temp\6731ed820b24e1de1ec5948b477ecd1.jpg)

**scanf两个规则**

* 如果scanf将转换的二进制存储到基本变量当中，请在**变量**名前加&
* 日如果scanf将字符串存储到字符数组中，**字符数组**名前不用加&

**用scanf输入字符和字符串**

其实就是将字符转化为ASCII码存进二进制里面，但是当输出出来的时候，要注意的是你要输出的是字符还是这个字符对应的ASCII码的十进制位数

而关于字符串的不考虑

```c
#include <stdio.h>
int main()
{
    char c;
    scanf("%hhd", &c);  // 存储到二进制  str[10]->字符数组
    printf("%d %c\n", c, c);  // 这里%d即输出数字，而%c则输出字符
    return 0;
}
```

## 五.运算符

### 5.1 表达式

表达式如以下

> 100；-->表达式语句
> 5 + 10；5、100为运算对象，+为运算符号
> a / b；
> a * 10 / b + c；

每个表达式必然要有个结果：printf("%d\n", 5 + 10); ->表达式结果为15，这里表达式为子表达式分号在printf后面

### 5.2 运算符

+运算对象的值：不可以改变运算对象正负，-运算对象的值：可以改变运算对象的正负

| 运算符号       | 运算符号代表意义                                             |
| -------------- | ------------------------------------------------------------ |
| +              | 相加，而“+运算对象”不可以改变运算对象的值正负                |
| -              | 相减，而“-运算对象”可以改变运算对象正负的值                  |
| *              | 相乘                                                         |
| /              | 相除，整除为整数，无法整除即为浮点，整型除整型依然是整型所以会被截断小数部分，这时整型要改为浮点 |
| %              | 求余符号，经常用于判断是奇数还是偶数                         |
| =              | 赋值运算符，给变量赋值：等号右边对象的值，传递给左边运算对象，int a = 100为变量初始化，所以要看是否声明了变量 |
| ==             | 等值运算符                                                   |
| 自增自减运算符 | ++：自增运算符，--为自减运算符，运算对象++ or 运算对象--：后缀模式，++运算对象 or --运算对象：前缀模式(主要看符号在运算对象的前后)，**前缀模式：a=10，b=10，++a：运算对象+1，--b：运算对象-1**额外对象还可以赋值，**后缀模式：a=10, b=10, a++, b--,此时先打印a++， b--实际均为原来的a， b，而当再次打印a，b此时变为a=11， b=9**。 |

i++(后缀模式)：先进行赋值在进行自增

++i(前缀模式)：先进行自增在进行给赋值



两种编译器对a++的额外作用的不同表达，什么时候额外使用的区别

> a = 1
>
> b = a++ + a++ + a++

**以下是VS的**

![c92ee4e8941d11951144087a1d7494d](C:\Users\DELL\Documents\WeChat Files\wxid_r87uet4wdjgp12\FileStorage\Temp\c92ee4e8941d11951144087a1d7494d.png)

VS累积所有子表达式求值后才会进行额外作用

**以下是GCC的**

![95e16f3b954a699bced808f70fb7d1b](C:\Users\DELL\Documents\WeChat Files\wxid_r87uet4wdjgp12\FileStorage\Temp\95e16f3b954a699bced808f70fb7d1b.png)

GCC每完成一个子表达式，则额外作用马上执行

这说明着：**额外作用在不同的编译器里面有不同的发生时机**，额外作用的最晚发生时机：完整表达式结束之后进入下一步之前，**前缀表达式和后缀表达式都会有不同的额外作用发生时机**所以不要在同一个表达式进行自增自减的多次

C的运算符优先级表格：优先级越高，则越被优先处理

![a08402cf95d28b7eaf16a6d97c4adaa](C:\Users\DELL\Documents\WeChat Files\wxid_r87uet4wdjgp12\FileStorage\Temp\a08402cf95d28b7eaf16a6d97c4adaa.jpg)



## 六.数据类型转换

### 6.1 同类型数据运算

> 高级别数据类型数据范围大于或等于低级别类型

**整型同类型运算：**

​	char <= short <= int <= long <= long long：所以在转换为整型中，比int级别低的数据类型运算会转为int，而比int数据类型高的数据类型运算保持不变

​	**关于无符号整形数据类型**：unsigned char <= unsigned short <= int <= unsigned int <= unsigned long <= unsigned long long

​	综上所述：比int级别低的类型会转化为int，比int级别高的类型都不会变

**浮点同类型运算：**

​	float <= double

​	浮点类型同类型同类型运算，数据类型是不会变的

### 6.2 **不同数据类型运算：**

1. 若两边运算符类型均低于或等于int，那么结果就是int
2. 如果高于int，则为高于int的等级最高的等级
3. 对于无符号，那么也和有符号是相同的
4. 有无符号混合运算，定义也是一定的
5. 浮点不同类型的结果为两边级别最高的类型
6. **浮点类型和整型类型运算：浮点类型高于任何的整型类型**，所以也为两边等级最高的类型

等级图如下所示：无符号的比有符号的数据类型要高

![9074d6c806c130105b1b7f51097c070](C:\Users\DELL\Documents\WeChat Files\wxid_r87uet4wdjgp12\FileStorage\Temp\9074d6c806c130105b1b7f51097c070.jpg)

整型运算注意事项，整型与整型运算，没有除尽的情况之下，是会截断小数部分，所以最好两个整型转为浮点类型，要么就是高数据等级运算使用float

### 6.3 强制类型转换

> 不会更改原来的数据的类型，只是在运算的时候加入短暂影响运算而已

```c
#include <stdio.h>
int main()
{
    int n1 = 5, n1 = 2;
    printf("%f\n", (float)n1 / n2);
    printf("%f\n", n1 / (double)n1=2);
    return 0;
}
```



 ## 七.关系运算符和逻辑运算符

### 7.1 关系运算符

> 用于判断数值之间的关系

**大于小于  > <**

```c
#include <stdion.h>
int main()
{
    printf("%d\n", 1 > 2);  // 运行结果：0--->False
    printf("%d\n", 1 < 2);  //          1--->True
    return 0;
}
```

**大于等于 >=   小于等于<=**

```c
#include <stdio.h>
int main()
{
    printf("%d\n", 1 >= 1);  // 运行结果：1--->True
    printf("%d\n", 1 <= 1);  //          1--->True
    return 0;
}
```

**等于==  不等于!=**

### 7.2 逻辑运算符

1. 表示x <= 2或x >= 10：或**||**  -----> **(x <= 2) || (x >= 10)**
2. 表示 2 <= x <= 10 ---> x >= 2 与 x <= 10： 与**&&** -----> **(x >= 2) && (x <= 10)**

**优先级比关系运算符要低**，平时写程序时两边括号可以直接去掉

**逻辑非 ! **：表示当前结果取反----->**(x >= 2) && (x <= 10)**取反**!((x >= 2) && (x <= 10))** -----> **(x < 2) || (x >10)**

**总的运算优先等级**: **++(--)前后缀** > **!** > **(+正号) -(负号)** > *** / %** > **+-(加减)** > **< > <= >=** > **== !=** > **&&** > **||** > **=**

## 八.分支结构

### 8.1 顺序流程

> 代码呈现线性，直下进行

### 8.2 分支流程(条件语句)

> if (测试条件)：
>
> ​	条件为真的流程

```c
#include <stdio.h>
int main()
{
    int x;
    scanf("%d", &x);
    if (2<=x && x<=10)  // if关键词
        printf("Yes\n");
    return 0;
}
```

**else**关键词

> if (测试条件)
>
> ​	条件为真执行流程
>
> else
>
> ​	条件为假执行流程

```c
#include <stdio.h>
int main()
{
    int x;
    scanf("%d", &x);
    if (x>=2 && X<=10)  // 不可以使用分号，要缩进，不然会变成空语句报错
        printf("Yes\n");
    else
        printf("No\n");
    return 0;
}
```

#### **复合语句**

```c
#include <stdio.h>
int main()
{
    int x;
    scanf("%d", &x);
    if (x>=2 && X<=10)  // 不可以使用分号，要缩进
    {
        printf("Yes\n");
        // 其他要进行的主要流程
    }    
    else
    {
        printf("No\n");
        // 其他继续执行的主要流程
    }
    return 0;
}
```

#### **嵌套语句**

伪代码如下：

```c
if (condition1)
{
    processing1
}
else
{
    if (condition2)
    {
        processing2
    }
    else
    {
        processing3
    }
}
```

正确代码如下：

```c
#include <stdio.h>
int main()
{
    int x;
    scanf("%d", &x);
    if (x<2)
    {
        printf("Left\n");
    }
    else  // 可以去掉这个else上的花括号，下面的if向上连接else
    {
        if (2<= x && x<=10)
        {
            printf("In\n");
        }
        else
        {
            printf("Right\n");
        }
    }
    return 0;
}
```

将上述的代码改为标注的位置

```c
#include <stdio.h>
int main()
{
    int x;
    scanf("%d", &x);
    if (x<2)
    {
        printf("Left\n");
    }
    else if (2<= x && x<=10)  // 这个else if 很想Python里面的elif，后面也要携带条件
    {
        printf("in\n");
    }
    else
    {
        printf("Right\n");
    }
    return 0;
}
```

#### **条件表达式(?:)**

#### 测试条件？表达式1：表达式2；根据条件表达式，如果测试条件为真，那就向表达式1；如果测试条件为假，那就向表达式2。**条件表达式的优先级仅仅高于赋值运算符**(三元切换条件)

> c = x >= 10 ?:  'Y': 'N';

### 8.3 循环流程

**求和**：sum=0,i=1 ----> i<=100 ---->真----> sum=sum+i ----> i++

​					|-------------<----------------<--------------|

#### while循环

```c
while (循环条件)
{
    循环行为1;
    循环行为2;
    循环行为4;
    …………
}
```

求1到100的求和

```c
#include <stdio.h>
int main()
{
    int i = 1, sum = 0;  // 为计数器设置初始值
    while(i<=100)  // 循环条件的问题
    {
        sum = i + sum;
        i++; // 更新计数器
    }
    printf("d/n", i, sum);
    return 0;
}
```

**关于循环条件的问题**：while(条件)，**在C语言里面，非0即为真**，所以只要while后面是个2那么就会变为不断的打印下去，所以**循环要有效**

#### for循环

**for循环伪代码**

```c
for(计数器设置初始值; 循环条件; 计数器更新)
{
    循环行为;
    循环行为1;
    循环行为2;
}
```

**1到100求和的for循环求解**

```c
#include <stdio.h>
int main()
{
    int i, sum = 0;  // 2.的条件下这里i也要变量初始化i = 1  3.的前半部分也要加在这i = 1
    for(i=1; i<=100; i++)  // 这里的for循环可以控for(;;),1.for(i=1;i<=100;),2.for(;i<=100;i++),3.for)(;i<=100;)
    {
        sum = sum + i;  //  1.的条件之下i++要在这里/3.的条件也是后半部分加在这里
    }
    print("%d %d\n", i, sum);
    return 0;  // 但是如果是循环没了就变成死循环就好比for中间部分没了
}
```

#### do 循环行为 while(循环条件)

伪代码如下

```c
do
{
    循环行为;
}while(条件)
```

do while实例代码

```c
#include <stdio.h>
int main()
{
    int x;
    do
    {
        scanf("%d", &x);  // 先执行一遍这里的条件，并保存至x
    }while(x < 0);  // 假如x继续小于0，则继续循环，直到不可以为止
    printf("%d\n", x);
    return 0;
}
```

### 8.4 嵌套循环

如下代码为一则内外循环的代码

```c
#include <stdio.h>
int main()
{
    for(char c = 'A'; c <= 'E'; c++)  //外循环
    {
        for(int i=0; i <= 9; i++) // 内循环
        {
            print("%c%d", c, i);
        }
        print("\n");
    }
    return 0;
}
```

### 8.5 循环辅助

#### 使用break打破循环

当前代码并没有使用break

```c
#include <stdio.h>
int main()
{
	int i = 0;
    while(i<10)
    {
        printf("%d", i);
        i++;
    }
    printf("%d", i);
    return 0;
}
```

**使用break**打破循环

```c
#include <stdio.h>
int main()
{
    int i = 0;
    while(1)
    {   //   <--------|
        if(i==10)  // |
        {  //         |
            break; // |
        }          // |
        printf("%d", i);  // 如果先于if语句那么会先在if之前打出一个10，如果像现在这个样那么在最后不会打出10，这是因为程序是从上而下的
        i++;
    }
    return 0;
}
```

#### 使用continue

>continue: 跳过本次循环，直接开始下一轮循环

```c
#include <stdio.h>
int main()
{
    int i = 0;
    while(i < 20)
    {
        if(i==6)
        {
            i = 15;
            continue;  // 最后结果是 1 2 3 4 5 15 16 17 18 19 
        }
        printf("%d", i);
        i++;
    }
    return 0;
}
```

#### for循环使用continue和break

```c
#include <stdio.h>
int main()
{
	for(int i=0; i < 20; i++)
    {
        if(i==6)
        {
            i = 15;
            continue;  // 1 2 3 4 5 16 17 18 19, 如果直接使用break则立即跳出循环，不会进入计数器进行运算
        }
        printf("%d", i);
    }
    return 0;
}
```

加入内置多个循环的break

```c
#include <stdio.h>
int main()
{
    for(;;)
    {
        for(;;)  // 2. /当这一层循环结束之后才会往下面的1.break
        {
            break;  // 这里结束的是2.的break
        }
        break;  // 1.之后这里结束之后才会return 0
    }
    return 0
}
```

## 九.多重选择

### 9.1 航空字符与字母的转化

| 字母 | 读法    |
| ---- | ------- |
| A    | alpha   |
| B    | bravo   |
| C    | charlie |
| D    | delta   |
| E    | echo    |
| F    | foxtrot |
| G    | golf    |

则有以下代码：

```c
#include <stdio.h>
int main()
{
    char letter:
    scanf_s("%c", &letter);
    if(letter=='a')
        printf("alpha\n");
    else if(letter == 'b')
        printf("bravo\n");
    else if(letter == 'c')
        printf("charlie\n");  // 输入如上的a,b,c,d,e,f,g
}
```

### 9.2 多重选择语句

```c
switch(整型表达式)
{
    case 整型常量1:
        语句
    case 整数常量2:
        语句
    …………    
}
```

于是则有以下的转化语句

```c
#include <stdio.h>
int mian()
{
    char letter:
    scanf_s("%c", &letter);
    switch(letter)  // switch里面只可以输入一个整型表达式
    {
        case 'a':  // case后面的常量不可以重复
            printf("alpha\n");
            break;  // --------当把break去掉后，假如输出一个a，那么a后面的全部打印，意味着case仅仅从当前的开始选，只有遇到break才可以结束，从而跳出，不然将执行你所选择的后面的输出以及自己输出的部分
        case 'b':
            printf("bravo\n");
            break;  // 输入直到g
        default:
            printf("idk")  // 这个default可以没有
    }
    return 0;
}  // 总而言之就是不断的将你输入的与case里面的表示
```

当加入循环以后：

```c
#include <stdio.h>
int main()
{
	char letter;
    while(1)
    {
        scanf_s("%c", &letter);
        switch(letter)  // switch里面只可以输入一个整型表达式
    	{
        	case 'a':  // case后面的常量不可以重复
           		printf("alpha\n");
            	break;  // --------当把break去掉后，假如输出一个a，那么a后面的全部打印，意味着case仅仅从当前的开始选，只有遇到break才可以结束，从而跳出，不然将执行你所选择的后面的输出以及自己输出的部分, 这里的break只属于switch语句
        	case 'b':
            	printf("bravo\n");
                getchar();  // 输入直到g
                continue;  // continue对switch无作用，属于while循环
        	default:
            	printf("idk");  // 这个default可以没有
        }
        getcahr();
        break;  // 这里的break只属于while
    }
    return 0;
}
```

## 十.初识数组

### 10.1 什么是数组

> 数组是由一系列类型相同的，数据对象一次排序而成，组成数组的数据对象被称做数组的元素

| 1    | 2    | 3    | 4    | 5    | 6    | 7    | 8    | 9    | 0    |
| ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |

**数组的特点**

1. 数组都是一次排列的，每个数组都是相邻的
2. 数组都是类型相同的数据对象，不同数据对象是不可以组成数组的

**声明变量和声明数组**

1. 声明**变量**——>数据类型 变量名——>char c; int n; long l; float f; double df
2. 声明**数组**——>元素类型 数组名[元素数量]——>char c[5]; int n[10]; long l[3]; float f[2]; double df[1]

**数组初始化**

变量的声明

```c
int n = 100;  // 初始化(变量声明)，这里的等号并不是赋值而是单纯的初始化，写作等号而已
n = 100  // 赋值
n = 456  // 重复赋值可以，不可以多次声明化
```

数组的初始化

**元素类型 数组名[元素数量] = {逗号分割元素内容}**

```c
int arr[10] = {1, 2, 3, 4, 5, 6, 7, 8, 9, 0};  // 为上面的表格符号——>初始化列表，逗号隔开，花括号抱起来
```

如果初始化数组的长度与括号内，内容不一样那么

```c
int arr[10] = {1, 2, 3, 4, 5}  // 数组变为{1, 2, 3, 4, 5, 0, 0, 0, 0, 0},若花括号内全为空则变成{0，0，0，0，0，0，0，0，0，0}
```

如果初始化数组的长度小于花括号内元素数量，那么代码是无法编译通过的

```c
int arr[10] = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11};  // 代码是无法编译通过的
```

如果不知道数组列表的花括号内有多少个元素，那么可以有如下表达

```c
int arr[] = {1, 2, 3, 4, 5}  // 这时候的数组会自动识别花括号的元素数量
```

**访问数组**：数组名[下标]

特别注意：下标是从0开始的，0代表数组中的第一个元素

```c
int arr[10] = {1, 2, 3, 4, 5, 6, 7, 8, 9, 0};
for(int i = 0; i < 0; i++)
{
    printf("%d\n", arr[i])
}  // 竖着排列1， 2， 3， 4， 5， 6， 7， 8， 9， 0
```

修改数组中的一个元素

```c
int arr[10] = {};
printf("%d\n", arr[5]);
arr[5] = 123;  // 跟python一样改变列表里面的东西
printf("%d\n", arr[5]);  
```

**数组越界问题**：访问数组超出了数组的长度，c编译器无法识别这一问题

```c
int arr[10] = {};
printf("%d\n", arr[10]);  // 按理来说是要运行到0-9之间，但是是10已经超出了10个数,越界出错
```

循环问题也要注意越界

```c
#include <stdio.h>
int main()
{
	int arr[10] = {1, 2, 3, 4, 5, 6, 7, 8, 9};  // 倘若数值没有初始化，会打印一些奇怪的值
    for(int i = 0; i <= 0; i++)  // 这里<=0会超出边界问题，导致编译错误，正确应该是<
    {
        printf("%d\n", arr);
    }
    return 0;
}
```

**注意**：__数组不一定初始化__，但是之后要赋值，避免无意义的数值

**数组所占用的大小**：单个元素占用的大小*数组元素的大小 = 数组所占的空间

**数组能整体赋值吗------>复制列表**

```c
int arr1[5] = {};
int arr2[5] = {1, 2, 3, 4, 5};
arr1 = arr2;
arr1 = {1, 2, 3, 4, 5};  // 初始化列表，只能存在于初始化之中，就是说现在列表已经是{}，不可能再是arr2的等职】值
```

1. 使用循环来赋值给另一个数组

   ``` c
   int arr1[5] = {};
   int arr2[5] = {1, 2, 3, 4, 5};
   for(int i = 1; i < 5; i++)
   {
       arr1[i] = arr2[i];
   }
   ```

2. 内存赋值(memcpy函数：memory copy)

   ```c
   #include <stdio.h>
   #include <memory.h>  // 要使用memory函数则要使用这个头文件
   int main()
   {
       int arr1[5] = {};
       int arr2[5] = {1, 2, 3, 4, 5};
       memcpy(arr1, arr3, sizeof(arr1));  // memcpy(arr1:目标数组名, arr2:原始数组名, sizeof(arr1):需要复制的数据)
       for(int i = 0; i < 5; i++)  // 假如需要复制n个元素，原始数组的大小不可小于N，否则将将复制无意义内容，目标数组大小不可小于n，否则没有足够空间存放数据
           printf("%d\n", arr1[i]);
       return 0;
   }
   ```




### 10.2 多维数组

#### 数组作为数组元素

数组A ------>int A[10]：生成十个元素的数组A

| int  | int  | int  | int  | int  | int  | int  | int  | int  | int  |
| ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |

数组B ------->??? -------> int[10] B[5] ------->int B[5] [10]

| int[10] | int[10] | int[10] | int[10] | int[10] |
| ------- | ------- | ------- | ------- | ------- |

#### 二维数组

类似python里面的列表嵌套列表  **B[i] [j]**: i 代表行数，j 代表列数

假如现在有个数组：int B[5] [10]

|      | 0           | 1           | 2           | 3           | 4           | 5           | 6           | 7           | 8           | 9           |
| ---- | ----------- | ----------- | ----------- | ----------- | ----------- | ----------- | ----------- | ----------- | ----------- | ----------- |
| B[0] | int [0] [0] | int [0] [1] | int [0] [2] | int [0] [3] | int [0] [4] | int [0] [5] | int [0] [6] | int [0] [7] | int [0] [8] | int [0] [9] |
| B[1] | int         | int         | int         | int         | int         | int         | int         | int         | int         | int         |
| B[2] | int         | int         | int         | int         | int         | int         | int         | int         | int         | int         |
| B[3] | int         | int         | int         | int         | int         | int         | int         | int         | int         | int         |
| B[4] | int         | int         | int         | int         | int         | int         | int         | int         | int         | int         |

```c
// 初始化一个数组
int B[5][10] = {
    {0, 1, 2, 3, 4, 5, 6, 7, 8, 9},
    {10, 11, 12, 13, 14, 15, 16, 17, 18, 19},
    {20, 21, 22, 23, 24, 25, 26, 27, 28, 29},
    {30, 31, 32, 33, 34, 35, 36, 37, 38, 39},
    {40, 41, 42, 43, 44, 45, 46, 47, 48, 49}
}
```

**类似于一维数组，当常量个数少于元素个数将使用0初始化元素**，**当然也可以省略里面的花括号**， **省略内层花括号时，如果元素的个数不足，后续的元素将使用0初始化**

可以使用嵌套循环来遍历二维数组

```c
#include <stdio.h>
int main()
{
	int B[5][10] = {
    {0, 1, 2, 3, 4, 5, 6, 7, 8, 9},
    {10, 11, 12, 13, 14, 15, 16, 17, 18, 19},
    {20, 21, 22, 23, 24, 25, 26, 27, 28, 29},
    {30, 31, 32, 33, 34, 35, 36, 37, 38, 39},
    {40, 41, 42, 43, 44, 45, 46, 47, 48, 49}
    };
    for(i=0; i < 5; i++)
    {
        for(j=0; j < 10; j++)
        {
            printf("%d", B[i][j]);
         }
        printf("\n");
    }
    return 0;
}
```

**修改二维数组元素和修改一维数组元素的方法是一样的**

### 10.3 更高维的数组

> int c[2] [5] [10]; ------------->数组名c，元素个数两个，元素类型int[5] [10]]

一般使用多重嵌套循环来访问数组的值

## 十一.字符数组

| H    | e    | l    | l    | o    | W    | o    | r    | l    | d    |                        |
| ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---------------------- |
| 72   | 101  | 108  | 108  | 111  | 87   | 111  | 114  | 108  | 100  | 0：数值0标记字符串结束 |

数值0和字符0不是一个概念，表格中的0是转义字符用\0表示

字符串满足以下特点：1. 类型相同  2. 顺序排列

### 11.1 **声明并初始化字符串数组**

```c
char str[20] = "HelloWorld";
char str[20] = {'H', 'e', 'l', 'l', 'o',
               'W', 'o', 'r', 'l', 'd'};  // 上述两则代码实际相同
```

打印字符串数组：1.printf(str)  2. printf("%s", str)

### 11.2 **字符数组后尾\0是否存在的问题**：

1. 初始化数组长度小于数组长度，数组末尾会不断的补上0，所以终归会有\0表示数组的结尾

   ```c
   char str[20] = {'H', 'e', 'l', 'l', 'o',
                  'W', 'o', 'r', 'l', 'd'};  // 等号后半部分才是初始化数组
   ```

2. 初始化数组长度等于数组长度，这时候实际数组打印出来会后面不断乱码，如果自己结束说明直到那里为\0

   ```c
   char str[10] = {'H', 'e', 'l', 'l', 'o',
                  'W', 'o', 'r', 'l', 'd'};  // 这里长度两边是相同的，会打印数组外的元素
   ```

3. 初始化数组长度大于数组长度，这时候会发生编译错误、

   ```c
   char str[5] = {'H', 'e', 'l', 'l', 'o',
                  'W', 'o', 'r', 'l', 'd'};  // 这时候会发生编译错误
   ```

### 11.3 **测量字符串长度**

```c
char str[20] = "helloworld";
printf("%d",sizeof(str));  // --------->这里字符串为20个字节， 无法正确测量字符串长度
```

**使用循环测量字符串长度**

```c
#include <stdio.h>
int main()
{
	char str[20] = 'helloworld';
    int len = 0;
    while(str[len] != '0')
    {
        len++;
    }
    printf("%d", len);
    return 0;
}
```

**使用strlen来测量字符串长度**

```c
#include <stdio.h>
#include <string.h>
int main()
{
	char str[20] = 'helloworld';
    int len1;
    len1 = strlen(str);  // ----->测量str字符串的长度----->10
    printf("len1 = %d\n", len1);
    
    int len2:
    len2 = strlen("helloworld");  // ----->测量字符串常量的长度
    printf("len2 = %d\n", len2);
    
    printf("sizeof str %d\n", sizeof(str));   // ------>20
    printf("sizeof str %d\n", sizeof("helloworld"));  // ------>11
    return 0;
}
```

Conclusion: strlen(str)：测量从第一个元素直到\0的字符串长度，sizeof(str)：测量数组本身占用的空间大小

### 11.4 修改字符串内容

**字符串常量不能修改，字符数组可以修改**

```c
#include <stdio.h>
#include <string.h>
int main()
{
	char str[20] = 'abcde';
    printf(str);
    printf("\n");
    for(int i = 0; i < strlen(len); i++)
    {
        str[i] = str[i] - 32;  // ASCII码转换，大写字母和小写字母差了32
    }
    printf(str);
    return 0;
}
```

### 11.5 输入字符串数组

利用scanf函数，注意对应的占位符为%s，scanf输入时没有\0------>字符串是可以正常结尾的

除此之外还可以有其他函数来输出输入字符：**putchar**(输出)--------> putchar('A')， **getchar**(输入字符)------------->char c; c = getchar()，**当前两个函数是对应字符串而言的**

## 十二. 输入和输出缓存

新需求

```c
#include <stdio.h>
#include <windows.h>
int main()
{
    for(int i = 0; i < 10; i++)
    {
        printf("helloworld %d", i);
        Sleep(500);  // 对比linux休眠函数不同而且时间也不同
    }
    return 0;
}
```

同样的代码，在不同的系统具有不同的效果

### 12.1 输出缓存区

输入，再往返出来均是批量处理：**累积一串字符再批量处理，比单个发送更有效率**

将数据发送至目的地并清空缓存，即刷新缓存

对比两个系统：

1. Windows系统 ------------>printf函数------------->输出缓存区----------------->立即刷新缓存

2. Linux系统计 ------------>printf函数 -------------->输出缓存区 ---------------->累积数据直到程序结束

   ​                                                                               |————————>遇到换行符，缓存区刷新

**行缓存**：一行结束之后必须刷新缓存，\n换行符代表一行结束

**完全缓存**：等到缓存区被填满才可以刷新缓存

输出缓存是系统特性，不是函数特性

输入缓存属于阻塞函数，只有按掉回车键也就是\n才会推出缓存区

```c
#include <stdio.h>
int main()
{
    char c1, c2;
    c1 = getchar();  // 这里面输入A ，enter键
    putchar(c1);  // 输出即为A，这时候缓存就有一个换行符\n，但此时这里之下加多一行getchar(),那么实际输出会变为A\AB\B,这里的换行键实际上一直存储在缓存里所以输出A\AB\B
    getchar();
    c2 = getchar();  // 这时候实际上已经输入了一个enter代表\n
    putchar(c2);  // 所以这里输出了一个\n
    return 0;
}
```

### 12.2 带缓存的输入函数

```c
#include <stdio.h>
int main()
{
    char str[20];  // 输入两个helloworkhellowork
    int i = 0;
    while(i < 20 - 1)
    {
        char c;
        c = getchar();
        str[i++] = c;
        if(c == '\n')
        {
			break;  // 当循环结束后这时候输出会变成helloworldhelloworl，缓存中存在这d
        }
	}
    str[i] = '\0';
    printf(str);
    scanf("%s", str);  // 而这时这里可以打出scanf，可以将str里面剩余的d输入进去
    printf(str);  // 打印输出，于是未识别到\n,继续打印d和\n,这时候输出才完全
    return 0;
}
```

CONCLUSION: 只有按下**enter**键时，输入的字符串才会进去输入缓存，等待程序进行读取

### 12.3 不带缓存的输入函数

> 不用按下回车即可输出字符

#### 12.3.1 get函数

> 无需回车，没有缓存区，get立刻获取对应字符，输入q当前立刻技术输入

#### 12.3.2 getche函数

> 会将输入的字符打印在控制台，无需再次调用putchar打印

**getche** 和 **getch**函数要记得使用头文件<conio.h> ------------->非标准头文件，默认使用"_"用于区分**平台实现函数**和**c语言标准函数**

![15683c25b8402e7dc05f7ae11e50946](C:\Users\DELL\Documents\WeChat Files\wxid_r87uet4wdjgp12\FileStorage\Temp\15683c25b8402e7dc05f7ae11e50946.jpg)

上图为综合使用getchar(带缓存)------>这个会按缓存位置逐次打印，但必须要继续putchar才会继续打印下去，getch(不带缓存)，以及用于区分代缓存和不带缓存



## 十三. 函数

### 13.1 函数的特性属性

> 建立一种方法，专门求解一类东西

```c
返回值类型 函数名(输入参数值);  // 函数头 ：每个参数要指明参数类型
{
	做点什么事情;  // 数体
    return 函数返回值;  // 数体
}
```

调用函数，以主函数为例

```c
#include <stdio.h>
int add(int a, int b)
{
    return a + b;
}

int main()
{
    int result;
    result = add(2, 3);  // 这里的主函数从这里调用了add函数，传入到add函数，result存放add函数的返回值
    printf("%d", result);
    return 0;
}
```

**为什么把代码封装成函数**：重复的代码调用到不同的文件

### 13.2 函数返回

```c
#include <stdio.h>
void showStars(void，)
{
	printf("     *\n");
    printf("    *  *\n");
    printf("  *   *  *\n");
    return;  // 返回类型为void即为空类型，参数的括号也可以是空的甚至可以填写一个void在里面，同时即表示函数不需要参数，一旦函数出现return起始函数已经算是结束了，不会再执行后面拥有的过程
}

int main()
{
	showStars();
    return 0;
}
```



### 13.3 函数声明

**假如主函数放在定义的函数之前，那么这个时候的主函数中会调用函数的话，因为放在了后面，所以就会识别不了函数，这时候就会编译错误**，至于解决这个问题，**其实可以将函数的声明先写在主函数前面，头文件之下，先声明函数，编译器就会正确识别**，其次这里的声明可以没有函数名，函数名在这里并不重要，所以可以使用与函数里面变量名不一致的也可以

```c
#include <stdio.h>
#include <math.h>
double areaOfTriangle(double, double, double);  // 函数声明
int isTriangle(double, double, double);
int main()
{
	double a, b, c;
    scanf("%f %f %f", &a, &b, &c);
    if(isTriangle(a, b, c) == 0)
    {
        printf("Not a Triangle");
        return 0;
    }
    double s;
    s = areaOfTriangle(a, b, c);
    printf("area of triangle %f", s);
    return 0;
}

double areaOfTriangle(double a, double b, double c)
{
	double p, s;
    p = (a + b + c)/2;
    s = sqrt(p * (p - a) * (p - b) * (p - c));
    return s;
}

int isTriangle(double a, double b, double c)
{
    if(a + b > c && b + c > a && a + c >b)
    {
        return 1;
    }
    return 0;
}
```

### 13.4 参数与返回值类型转换

```c
#include <stdio.h>
int add(int a, int b)  // 这里的a,b时形参
{
    return a + b;
}

int main()
{
    int result;
    result = add(2, 3);  // 2， 3是实际参数，一般来说形参和实参的形式应该要一致，但也可以不同，假如2.2，3.3传入里面去，数据可能会丢失，如2.2，3.3----->这里结果就变成了5少了0.5，所以数据类型转换了
    printf("%d", result);
    return 0;
}
```

**另外：形参和实参是相互独立的！**，**不同函数的参数也是互相独立的**

CONCLUSION：

1. 函数内声明的变量为局部变量
2. 不同函数的局部变量是相互独立的
3. 一个局部变量在另一个函数中使用，可以把它当作一个参数，传递它的值到另一个函数中

## 十四.函数递归

### 14.1 函数递归的使用

> 顾名思义函数自己调用自己

1. 递归规则
2. 递归结束条件

```c
#include <stdio.h>
void func(int n)
{
    if(n == 5)
        return;  // 当n为五时，递归结束
    printf("before %d\n", n);
    func(n + 1);  // 死循环一个，形成环形，ctrl+c结束循环，缺少递归结束条件
    printf("after %d\n", n);  // 因为递归在这串代码的上面所以func在未到五的时候一直递归，直到达到递归结束条件才会顺序继续下面的代码
}

int main()
{
	func(0);
    return 0;
}
// 在一个程序语言当中，函数可以自己调用自己的方法，叫做“函数递归“
```

### 14.2如何正确使用递归

```c
#include <stdio.h>
int func1(int n)
{
    if (n == 0 || n == 1)
    {
    	return 1;    
    }
    return f(n-1) * n;  // 递归过程
}

int main()
{
	int result = func1(5);
    printf("%d\n",result);
    return 0;
}
```

## 十五.调试代码

> 调试：排除程序的错误和缺陷的过程
>
> 1. 交互式调试
> 2. 控制流分析
> 3. 单元测试
> 4. 集成测试
> 5. 日志文件分析
> 6. 内存分析

### debug

> 默认情况下：1. 可执行文件未经过优化  2. 附带调试信息  3.链接运行库是调试版本  4.目标用户：程序员  5. 更强的调试能力

### release(发行版)

> 默认情况下：1. 可执行文件经过优化  2. 不附带调试信息  3. 链接运行库是发行版本  4.目标用户：使用者  5. 更小的体积和更快的速度

### 调试步骤

**打断点**

自动窗口：可以显示变量以及其他的值，显示在当前断点的变量

局部变量：显示定义在局部作用域内的变量

### 逐语句和逐过程的区别

逐语句：遇到函数则会进入函数的过程中

逐过程：遇到函数，执行完整个函数



## 十六.指针(C语言的精髓)

### 16.1 基础数据类型所占用的字节

| 数据类型  | 占用字节大小 |
| --------- | ------------ |
| char      | 1            |
| short     | 2            |
| int       | 4            |
| long      | 4            |
| long long | 8            |
| float     | 4            |
| double    | 8            |

以int数据为例，int占用的第一个字节的数据对象叫做**首地址**，而int数据类型需要占用4个字节，就是为**占用空间大小**

CONCLUSION：因此记录一个对象在内存中的存储位置，需要两个信息**1.数据对象的首地址** **2. 数据对象占用存储空间的大小**

### 16.2 指针数据类型

#### 16.2.1 取地址运算符“&”

> 可以获取数据对象的首地址和需要的存储空间大小

```c
int n;
类型 pn = &n;  // 获取数据对象的首地址和所需空间大小
```

**从上述类C的伪代码来看，pn即存储了n的首地址和需要的空间大小，所以即可通过pn找到变量n**

#### 16.2.2 声明指针类型的变量

```c
int n;
int*pn = &n;

char c;
char* pc = &c;
```

相关公式

**目标类型  *  变量名**

注意：1. 数据类型决定了数据的占用内存空间大小  2. 而变量存储在的变量名**"pc"**决定了数据对象的首地址

#### 16.2.3 取值运算符“*”

> 可以根据指针中存储的首地址和空间大小找到目标数据对象

```c
int n = 123;
int*pn = &n;
printf("%u\n", pn);   // 打印n的首地址
printf("%d\n", *pn);  // 根据pn中的首地址和空间大小，找到数据对象的值
```

#### 16.2.4 指针类型的大小

```c
#include <stdio.h>
int main()
{
    int n = 0;
    int* pn = &n;
    
    char c = 0;
    char* pc = &c;
    
    printf("sizeof pn = %d\n", sizeof(pn));
    printf("sizeof pc = %d\n", sizeof(pc));
    /*这里的指针地址的位数取决于电脑的位数，如果是x64的即为64位，1个数据8个字节，如果是x86,即为32位，一个数据32位，无论如何指针都代表表达所有内存地址的能力*/
}
```

尽管如此，char和int存储的是数据不同的两种数据，char存储小一点的整数范围，int存储大一点的数据范围，所以char可以占用小一点空间，而int占用大一些的空间

而char* 和 int*存储对象均为数据对象地址，所以占用空间是相同的，所以上述代码输出结果均为4

#### 16.2.5 强制转换下的指针类型

```c
#include <stdio.h>
int main()
{
    int n = 1431655765;
    int* pn = &n;
    char* pc = (char*)pn;
    
    printf("pn = %u\n", pn);  // 数据占用的首地址
    printf("pn = %u\n", pc);  // 数据占用的地址，与上面相同取决于电脑的位数
    
    printf("n = %d\n", n);   // 打印了n的值
    printf("*pn = %d\n", *pn);  // 打印了n的值，即通过pn的数据地址和占用空间大小
    printf("*pc = %d\n", *pc);  // 打印了n的值，可是char占用了一个字节，int四个所以两者结果不一样
    return 0;
}
```

上述对象主要是数据类型的不同而导致的

### 16.3 指针运算

> 指针类型存储两个重要的信息：1. 指针类型通过值来保存目标数据对象的首地址  2. 数据类型本身标记数据占用内存大小(int*)

```c
/* --记住  */
int main()
{
	int*; // 代表指针类型
    int* p = &n;  // 声明指针类型
    p; // p代表着获得的首地址
    *p;  // 代表获得的数据的值
}
```

**错误示范**

```c
#include <stdio.h>
int main()
{
    char* pc;
    short* ps;
    int* pn;
    long* pl;
    long long* pll;
    float* pf;
    double* pd;
    
    /* 这里的赋值是属于整数类型的而不是指针类型，主要是把数据的首地址赋值为100了 */
    pc = 100;
    ps = 100;
    pn = 100;
    pl = 100;
    pll = 100;
    pf = 100;
    pd = 100;  // 全部是整数类型的数赋值
    
    /* 地址加1 */
    pc = pc + 1;
    ps = ps + 1;
    pn = pn + 1;
    pl = pl + 1;
    pll = pll + 1;
    pf = pf + 1;
    pd = pd + 1;
    
    printf("pc = %u\n", pc);
    printf("ps = %u\n", ps);
    printf("pn = %u\n", pn);
    printf("pl = %u\n", pl);
    printf("pll = %u\n", pll);
    printf("pf = %u\n", pf);
    printf("pd = %n\n", pd);
    return 0;  // 最后编译器会提醒int类型无法转换指针类型
}
```

这时候的编译过程会说指针类型和整数类型无法互相转换，只有在pc = 100之间改为pc = (char*)100这时候就会由原来的整数类型转换为指针类型，原因就是100可以作为首地址，但没有明确的数据类型占用内存的空间

```c
/* 正确示范 */
#include <stdio.h>
int main()
{
    char* pc;
    short* ps;
    int* pn;
    long* pl;
    long long* pll;
    float* pf;
    double* pd;
    
    /* 这里的赋值是属于整数类型的而不是指针类型，主要是把数据的首地址赋值为100了 */
    pc = (char*)100;
    ps = (short*)100;
    pn = (int*)100;
    pl = (long*)100;
    pll = (long long*)100;
    pf = (float*)100;
    pd = (double*)100;  // 在前面加上“数据类型*”即强制转换为指针类型
    
    /* 地址加1 */
    pc = pc + 1;
    ps = ps + 1;
    pn = pn + 1;
    pl = pl + 1;
    pll = pll + 1;
    pf = pf + 1;
    pd = pd + 1;
    
    printf("pc = %u\n", pc);
    printf("ps = %u\n", ps);
    printf("pn = %u\n", pn);
    printf("pl = %u\n", pl);
    printf("pll = %u\n", pll);
    printf("pf = %u\n", pf);
    printf("pd = %n\n", pd);
    return 0;  // 最后编译器会提醒int类型无法转换指针类型
}
```

而关于指针类型的加减

#### 16.3.1 指针的加减实际上是首地址的加减

```c
sizeof(char) = 1;
sizeof(short) = 2;
sizeof(int) = 4;
sizeof(long) = 4;
sizeof(long long) = 8;
sizeof(float) = 4;
sizeof(double) = 8;
```

CONCLUSION：**在指针类型上加1，如果指针类型是char类型指针那么其加1即为首地址加上1个字节即1位，而如果是指针类型是int类型指针那么加1即为首地址加上4个字节，即加上4位，按照上面数据类型每每增加一个位，就加上相应数据类型的字节位，指针的减法运算也是同样道理。**

​	**指针类型加n后。首地址向后移动 n * 步长 字节。 指针类型减n后。首地址向前移动 n * 步长 字节。**

### 16.4 数组与指针

> 数组当中每个数据对象都是连续排布的，所以**数组第一个元素即为整个数组的首地址，可以通过取地址运算符“&”来获取元素的首地址和空间大小

```c
#include <stdio.h>
int main()
{
    int arr[5] = {111, 222, 333, 444, 555};
    for(int i=0; i < 5; i++)
    {
        printf("arr[%d]");
    }
    return 0;
}
```

#### 16.4.1 利用指针指向数组

```c
#include <stdio.h>
int main()
{
    int arr[5] = {111, 222, 333, 444, 555};
    int* p = arr[0];
    printf("%d\n", *p);
    printf("%d\n", *(p+1));
    printf("%d\n", *(p+2));
    printf("%d\n", *(p+3));
    printf("%d\n", *(p+4));
    return 0;
}
```

这里的数组的第一个元素111即为数组的首地址以及空间大小,p+1即为下一个

#### 16.4.2 指针数组的位数上的关系

```c
#include <stdio.h>
int main()
{
	int arr[5] = {111, 222, 333, 444, 555};  // 声明数组
    
    int* p = arr;  // 声明数组的指针
    printf("sizeof arr = %d\n", sizeof(arr));  // 这里打印的是一个数组的长度，111作为int类型占用了四个字节，五个数据总共20个字节长度
    printf("sizeof p = %d\n", sizeof(p));  // 而这里打印的是指针的长度，根据电脑的位数来决定的
    printf("sizeof arr + 1 = %d\n", sizeof(arr + 1));  // 这里的打印的又是指针的长度对此有以下的规则
    return 0;
}
```

**规则**

> T arr[5];  // 以T为元素的数组arr
>
> T *p;  // 指向T的指针

当数组名arr出现在一个表达式当中，数组名arr将会被转换为指向数组第一个元素的指针。但是，这个规则有两个意外：1. 对数组名arr使用sizeof时候 2. 对数组名使用&时候

在前者arr是int[5]，所以sizeof(arr)的结果才会是20，而对于后者arr出现在表达式int* p = arr中，会被转换成指向数组第一个元素的指针，即int[5]转换成了int* 。之后进行赋值运算

#### 16.4.3使用指针访问数组元素等价于下标访问

##### 一. 

1. 数组名[下标]
2. *(数组名 + 偏移量)----->偏移量：指针指向的地址与数组首地址之间相差的元素

示例如下

```c
#include <stdio.h>
int main()
{
    int arr[5] = {111, 222, 333, 444, 555};
    
    printf("arr[2] = %d\n", arr[2]);  // -----> 解析为*（arr + 2)
    printf("2[arr] = %d\n", 2[arr]);  // -----> 解析为*(2 + arr)
    printf("*(arr + 2) = %d\n", *(arr + 2));
    return 0;
}
```

### 16.5 指针作为参数传递

#### 16.5.1 探究实参和形参的相互独立

函数与主函数的参数相互独立，在函数中如果有两个形参x, y，但是却无法影响主函数已经进行过的实参赋值，所以无法影响到主函数中的变量

```c
#include <stdio.h>
void swap(int x, int y)
{
    int temp = x;
    x = y; 
    y = temp;
}

int main()
{
    int a, b;
    int temp;
    a = 1;
    b = 2;
    
    printf("a = %d b = %d\n", a, b);
    swap(a, b);
    printf("a = %d b = %d\n", a, b);
    return 0;
}
```

从一定上的意义来说上述的数据虽然是发生了调换，但依然函数内部的参数是无法影响到主函数当中的a，b两个变量的

现在进行取地址运算符

```c
#include <stdio.h>
void swap(int x, int y)
{
    /* 打印首地址 */
    printf("&x = %u\n", &x);
    printf("&y = %u\n", &y);
    
    int temp = x;
    x = y; 
    y = temp;
}

int main()
{
    int a, b;
    int temp;
    a = 1;
    b = 2;
    
    printf("a = %d b = %d\n", a, b);  // &a = 10484860
    swap(a, b);                       // &b = 10484856
    printf("a = %d b = %d\n", a, b);  // &x = 10484832
    return 0;                         // &y = 10484836  四个都是为两种参数的储存地址，各不相同
}
```

接下来通过指针的迂回战术，用指针进行数值的转换

```c
#include <stdio.h>
void swap(int* x, int* y)
{
    int temp = *x;
    *x = *y; 
    *y = temp;
}

int main()
{
    int a, b;
    int temp;
    a = 1;
    b = 2;
    
    printf("a = %d b = %d\n", a, b);
    swap(&a, &b);
    printf("a = %d b = %d\n", a, b);
    return 0;
}
```

对比前面没有任何***：取值运算符** 和 **&：取地址运算符**综合来看其实swap函数当中的两个变量相当于声明初始化了为指针类型，这里是直接声明了指针的类型

```c
/* 类似如下面这种声明 */
int* x = &a;
int* y = &b;
```

所以这则代码的实际则变为了一则关于将a的地址存储在指针x里面，b的地址存储在了指针y里面，原来x和y的地址发生了被a，b取代的问题，所以对于scanf函数中的**&变量**，是先将变量指针传入scanf中，通过指针使得被调函数间接地修改专属里面的变量

#### 16.5.2 指针不止是地址，更还有数据占用空间的大小

指针的值保存着数据的首地址，指针类型对应着目标数据对象的类型，用于标记目标数据对象的空间大小和指针运算步长

| 指针类型  | 目标数据长度      | 运算时步长        |
| --------- | ----------------- | ----------------- |
| char*     | sizeof(char)      | sizeof(char)      |
| short*    | sizeof(short)     | sizeof(short)     |
| int*      | sizeof(int)       | sizeof(int)       |
| long*     | sizeof(long)      | sizeof(long)      |
| long long | sizeof(long long) | sizeof(long long) |
| float*    | sizeof(float)     | sizeof(float)     |
| double*   | sizeof(double)    | sizeof(double)    |



#### 16.5.3 只有首地址的指针类型 void*

指针类型会锁死指向的数据类型

> void swap(void* x, void* y, int size)

int*修改为void*，类型为void*仅仅保存首地址，不保存数据类型的占用空间大小，所以无法对void *进行取值，因为指针的数据类型所以没有步长，因此不可实现指针类型的加减运算

**任意类型的指针可以直接赋值给只有首地址的的指针，但其他类型不可以相互赋值**

```c
char* pc;
int* pn;
pc = pn; // 数据的类型不同
    
void* p;
p = pn;
p = pc
```

CONCLUSION：1. 不同指针类型不能相互赋值，相互赋值后会造成目标数据对象的改变，无法通过编译 2. void*为特例，可以接受任意指针的赋值，也可以赋值给任意指针

**C语言当中void * 除了接受任意类型的指针，还可以自动转换，而C++仅能接受，不可自动转换为其他类型的指针

### 16.6多级指针和指针数组

#### 16.6.1 指针的指针

> 用一个指针取了一个数据的首地址，而关于这个指针是否还可以用另一个指针指代前者的第一个指针

```c
#include <stdio.h>
int main()
{
	int n = 123;
    int* pn = &n;
    int** pnn = &pn;
    
    printf("**pn = %d\n", **pnn);
    return 0;  // 得出结果也为123
}
```

取地址过程：该过程为对n使用取地址运算符，获取n的指针pn，类型int*，对pn使用取地址运算符，获取pn的指针pnn，类型为int **

取值过程：先对pnn使用取值运算符，将int ** 还原成int *，对 *pnn使用取值运算符，将int *还原成int

#### 16.6.2 指针数组

```c
/* 普通数组 */
int arr1[5] = {1, 2, 3, 4, 5};
int arr2[5] = {11, 22, 33, 44, 55};
int arr3[5] = {111, 222, 333, 444, 555};
```

上述均代表有五个元素的数组

下面将三个数据转换为首元素的指针存储再int* 数组里

```c
int* pToArr[3];
pToArr[0] = arr1;  // 转换为arr1的首地址即第一个元素代表数组的首地址
pToArr[1] = arr2;  // 转换为arr2的首地址即第一个元素代表着数组的首地址
pToArr[2] = arr3;  // 转换为arr3的首地址即第一个元素的首地址
```

**注意：pToArr是一个数组，由于是指针类型int *，所以被称为指针数组**

```c
#include <stdio.h>
int main()
{
    int* pToArr[3];
	pToArr[0] = arr1;  // 转换为arr1的首地址即第一个元素代表数组的首地址
	pToArr[1] = arr2;  // 转换为arr2的首地址即第一个元素代表着数组的首地址
	pToArr[2] = arr3;  // 转换为arr3的首地址即第一个元素的首地址
    for(int i = 0; i < 3; i++)
    {
        int** p = pToArr + i;  // 这里实在遍历三组数组
        for(int j = 0; j < 5; j ++)  // 这里是数组内部进行再遍历
        {
			printf("%d", *(*p + j))
        }
    }
}
```

1. p，指向pToArr的第一个元素，类型int **
2. *p，指向arr1的第一个元素，类型为int *
3. *p + j，指向arr1的第j个元素，类型为int *
4. **(* *p + j)，指向arr1中第j个元素，这里是直接取值了。

#### 16.6.3 从函数返回指针

```c
void func(int** a, int** b)  // 二级指针的函数标写
{
    static int x = 100;
    static int y = 100;
    *a = &x;  // int** 转换为int* ，在赋值一个int*给他即x的地址
    *b = &y;
}

int main()
{
    int* a = NULL;  // 一级指针
    int* b = NULL;
    func(&a, &b);  // 获取指针的地址
    if(a != NULL && b != NULL)
        printf("a = %d b = %d", *a, *b);
    return 0;
}
```

二级指针作为参数传入到func参数里面，通过返回时是根据赋值，进行指针的地址赋值，最后通过查询数据的内存地址，以及占用内存的空间大小进行返回

**进行函数编写的时候，每个函数之间是独立的，要使得每次函数之后内部的参数要有所保留，以防被回收时需要在声明的变量前面增加一个static**

我的理解主函数里面的&a和&b分别取到了指针变量a和b的又一个地址即为指针的指针，而外部函数func中的变量声明的int**为说明是内部参数a和b为指针的指针所以对应着&a和&b的，所以当外部函数使用到 *a实际上已经是回归到主函数的a的层面上来，说明a已经是内部函数声明过x的值的地址以及数据种类(表示存储空间的大小)，因此对应着主函数里面的a两者条件都有对其进行取值即可有函数返回指针

### 16.7 指针与多维数组

#### 16.7.1 声明数组

> 1. 数组名
> 2. 数组元素类型
> 3. 元素数量

**元素类型 数组名[元素个数]……**：通过在后面不但标注数组元素内部个数可以表示多维数组

#### 16.7.2 数组名转换规则

当数组名arr出现在一个表达式中，数组arr将会被转化为指向数组首元素的指针形同前文有个类似***(arr + 2)**的表达式

两个例外：1. 对数组名arr使用sizeof  2. 对数组名使用&时候

#### 16.7.3 多维数组和指针

```c
#include <stdio.h>
int main()
{
	int A[10];
    int B[5][10];
    printf("sizeof A = %d", sizeof(A));  // 打印出值为40   ----->int为字节数4有10个元素
    printf("sizeof B = %d", sizeof(B));  // 打印出值为200  ----->4*5*10
    return 0;
}
```

对于多维数组的声明

> int[10] B[5]和int B[5] [10]均代表着数组

对于A数组的声明：

> int* pA = A，代表着A数组的指针

对于多维数组B的声明：

> int[10] *  pB = B ---> int* pB[10]

声明一个数组：

| 元素类型 | 数组名 | [元素个数] | [元素个数] |
| :------: | ------ | ---------- | ---------- |

若元素类型中有括号移动到最右边

声明一个指针

| 目标类型 |  *   | 变量名 | [元素个数] |
| :------: | :--: | :----: | :--------: |

若目标类型中有方括号移动到右边

像上面的int * pB[10] 实际上时指针数组，但实际我们需要的是数组指针

于是有以下声明数组与指针的公式：**目标类型  ( * 变量名) [元素个数]**，目标类型如果有方括号全部右边移动

#### 16.7.4 数组指针的移动

```c
#include <stdio.h>
int main()
{
	int B[5][10] = {
        {0, 1, 2, 3, 4, 5, 6, 7, 8, 9},
        {10, 11, 12, 13, 14, 15, 16, 17, 18, 19},
        {20, 21, 22, 23, 24, 25, 26, 27, 28, 29},
        {30, 31, 32, 33, 34, 35, 36, 37, 38, 38},
        {40, 41, 42, 43, 44, 45, 46, 47, 48, 49},
    };
    int (*pInt10)[10] = B;  // 可见实际上数组指针是一个在B上内部五个数组的表达
    /* 移动1相当于移动4*10----->int一个数据占用4个字节 */
    printf("pInt10 = %d\n", pInt10);
    printf("pInt10 + 1 = %d\n", pInt10 + 1);
    printf("pInt10 + 2 = %d\n", pInt10 + 2);
    printf("pInt10 + 3 = %d\n", pInt10 + 3);
    printf("pInt10 + 4 = %d\n", pInt10 + 4);
    return 0;
}
```

可以通过pInt10的移动，我们可以使得指针在目标数据对象在各个数组切换

#### 16.7.5 对数组指针取值

> *pInt10：一样式取值的唯一方法

```c
#include <stdio.h>
int main()
{
	int B[5][10] = {
        {0, 1, 2, 3, 4, 5, 6, 7, 8, 9},
        {10, 11, 12, 13, 14, 15, 16, 17, 18, 19},
        {20, 21, 22, 23, 24, 25, 26, 27, 28, 29},
        {30, 31, 32, 33, 34, 35, 36, 37, 38, 38},
        {40, 41, 42, 43, 44, 45, 46, 47, 48, 49},
    };
    int (*pInt10)[10] = B;  // 可见实际上数组指针是一个在B上内部五个数组的表达
    /* 移动1相当于移动4*10----->int一个数据占用4个字节 */
    printf("B = %d", sizeof(B);  // 数组的长度----->200
    printf("pInt10 = %d\n", sizeof(pInt10));  // ------>指针的大小，与电脑位数有关
    printf("*pInt10 = %d\n", sizeof(*pInt10));  // ---->数组指针的大小，已经是10个数组的第一个进行取值，存储首元素，代表每一个数组------>所以是40---->4*10：属于数首元素指针
    return 0;
}
```

在这里当中pInt既是一个指针也是一个数组，所以是一个数组指针，当对pInt进行取值的时候即为一个数组

```c
#include <stdio.h>
int main()
{
	int B[5][10] = {
        {0, 1, 2, 3, 4, 5, 6, 7, 8, 9},
        {10, 11, 12, 13, 14, 15, 16, 17, 18, 19},
        {20, 21, 22, 23, 24, 25, 26, 27, 28, 29},
        {30, 31, 32, 33, 34, 35, 36, 37, 38, 38},
        {40, 41, 42, 43, 44, 45, 46, 47, 48, 49},
    };
    int (*pInt10)[10] = B;  // 可见实际上数组指针是一个在B上内部五个数组的表达
    printf("pInt10 = %d\n", pInt10); // 这时候打印出来第一个数组的首地址
    printf("pInt10 + 1 = %d\n", pInt10 + 1);  // 这时候为第二个的首地址
    
    int* pInt = *pInt10;  // 这时候是对pInt10进行取值------>为一个数组，让一个指针pInt指向数组的首元素
    printf("pInt = %d\n", pInt);  // 这里打印的数组B的第一个数组{0, 1，……}第一个0的地址即当前数组的首地址
    printf("pInt + 1 = %d\n", pInt + 1); // 以数组B内的第一个数组{0，1，……}为例打印的是第二个1的地址 --->指向B[0]的第二个元素
    /*……*/
    return 0;
}
```

pInt + 9指向B[0]的最后一个元素

pInt + 10指向B[1]的第一个元素

pInt + 11指向B[1]的第二个元素

**任何数组在内存的位置中都是连续的，二维数组也一样**

pInt + 11和pInt10 + 1两者的位置是相同的证明了这一点

#### 16.7.6 指针访问与下标访问等价

> 访问数组元素的两种方法：
>
> 1. 数组名[下标]
> 2. *(数组名 + 偏移量)

实际上这两种东西是等效的，通过两种方式的对比，都并不是直接对数组名进行运算，而是对数组名转换后的指向首元素的指针

上述定义的指针pInt10是指数组指针，pInt是这个数组里面的又一个指针

> (*plnt10)[i] = *(plnt + i)  = pInt[i] = A[i] [j]

#### 16.7.7 对数组取地址

当数组名arr出现在一个表达式当中，数组名arr将会被自动转换为指向数组首地址的指针，除了两个规则 1. 对数组arr使用sizeof  2. 对数组arr使用&

**&表示对一个数组或者变量取地址，数组不会进行类型转换，相反会直接取地址**

譬如：对int类型取地址会取为int(*)的指针，对int[10]会取int(**)[10]的指针

如以下

```c
#include <stdio.h>
int main()
{
    int arr[10];
    int (*pInt10)[10] = &arr;
    printf("pInt10 = %d\n", pInt10);
    printf("pInt10 + 1 = %d\n", pInt10 + 1);
    return 0;
}
```

可以清楚地看见对于这串代码，取的式数组指针，内部十个元素，int类型每个4个字节，所以步长为40

如果再取指针

```c
int arr[10];
int(*pInt10)[10] = &arr;
int(**pInt10)[10] = &pInt10
```

则表示arr数组里面藏了个用一级指针pInt10指代的数组有十个元素，而对于一级指针内的单个数组有藏了一个有十个元素的数组为二级指针pInt10所指代。清晰地话可以认为已经是三维数组了

### 16.8  声明器

#### 16.8.1 声明器的定义

> 提供**标识符**和**类型信息**，用于声明一个标识符的语法叫做声明器

```c
/* 声明器表达 */
int A[10];
int b = 10;
```

#### 16.8.2 声明与使用形式统一

> C语言设计者愿景：一个标识符的声明与使用统一

以为例子

```c
int A[10];  // 数组A的声明：标识符声明中的方括号内天数组长度
int n = A[0];  // 数组A的使用：标识符使用中的方括号内填元素下标
```

#### 16.8.3 函数声明器

```c
int* func(char*p, double d);
```

相关参数如下：

1. 第一个参数为char*类型
2. 第二个参数为double类型
3. 返回值为int*类型

#### 16.8.4 声明器中的优先级

一. 不同类型的指针和数组的结合

1. 基础类型：int*、 double*
2. 指针的指针：指向int * 的指针 int**
3. 数组指针 int (*)[5]
4. 指针数组 int *arr[5]：拥有五个元素都为指针的数组

个人见解：我严重怀疑指针和数组在C语言里面就好比对比Python的列表元素之间就是手动档位和自动挡的区别

#### 16.8.5 声明器优先级如下

1. 括号()
2. 函数声明的括号()和数组声明的方括号[]
3. 指针声明*

编译器会根据声明器以上优先的等级排序进行相关的编译，否则优先级相同的则会按照从左至右进行编译

##### 16.8.5.1 数组[ ]与指针*

1. 指针数组 int *a[5]
   * 数组[]的优先级高于指针的* --->数组
   * 接着计算数组[]，这个指针指向数组的首元素即首地址
2. 数组指针 int (*)[5]
   * 优先计算()里面的，于是显示一个指针
   * 然后优先度就到了[]，指针指向一格数组
   * 最后就是到指针然后指向数据类型

例子：标识符 int* (* id)[4]

先是使用取值运算符* ，将id指针转换为数组，可此时目前int前面还有一个* 则又转换为了指针，其实最后可以通过数据在* 星号取值即可获得外部指针的值，总体来说是将一个作为指针的数组又变回为指针的第一个元素的地址

##### 16.8.5.2 函数( )与指针*

```c
/* 函数声明与指针一起出现在声明器 */
int *func(char *, double);
```

1. 函数( )的优先级最高，所以当前为一个函数的声明
2. 函数里面的char指针和双精度浮点为函数的数据对象
3. int * 表示返回的是得出函数值的一个指针

```c
int (*func)(char*, double);
```

声明器当中出现了两个括号，优先级最高位(*func)

1. 优先计算括号( )内的指针，所以是一个指针声明
2. 接着计算函数( )，上一步的指针指向一个函数
3. 函数内部的char指针类型，双精度浮点是这个函数的参数
4. 最后函数返回为int

所以在这一条代码中func为一个指针，指向一个int(char * , double) ----->函数指针

### 未完待续

## 十七.Const 关键词

```c
#include <stdio.h>
int main()
{
	const char str[20] = "hello\n";  // 放在数据类型左右两边都不行
    printf("%s", str);
    str[0] = 'H';
    printf("%s", str);
}
```

const一用上之后则无法进行改变变量的做法，只会被读取

```c
#include<stdio.h>
int main()
{
	const char* pStr = "hello\n";  // 修饰指针指向的数据也就是就是hello这个玩意
    char const* pStr = "hello\n";  // 与上面的相同
    char * const pStr = "hello\n";  // 这个修饰指针的本身也就是地址数据在内存的位置
}
```

总结：const如果是在指针*的右边则表示的式地址不可发生改变，当然也可以对基础变量进行修改

## 十八.字符串处理函数

> 处理字符串的头文件必须加：#include<string.h>

#### 18.1 strlen函数

> 获取字符数组中的字符串长度，直至遇到**“\0”**

与sizeof的区别：sizeof主要反映数据的占用空间大小，strlen主要是一整个字符串的长度

#### 18.2 strcat函数

> 将两个字符串进行拼接的函数

```c
char scr1[9] = "ILove";
char scr2[4] = "You";
strcat(scr1, scr2);  // ILoveYou
```

这里的scr1是目标字符，目标字符的空间必须要大于你要拼接的长度，否则就会报错

#### 18.3 strcpy函数

> 将一个字符串复制到另一个上面

```c
char scr1[9] = "ILove";
char scr2[4] = "You";
strcpy(scr1, scr2);  // You
```

同理该函数也要注意目标字符串接受的空间要足够大

#### 18.4 strcmp函数

> 将两个字符串进行对比，一致返回0，否则返回其他值，主要是因为ASCII码到最后如果不一样则打印与\0和其余的末尾差值在ASCII码上有所表示

```c
#include<string.h>
#include<stdio.h>
int main()
{
	const char* str1 = "abcdefg";
    const char* str2 = "abcdefgh";
    const char* str3 = "abcdef";
    
    int ret = strcmp(str1, str1);  // 0
    printf("%d\n", ret);
    
    ret = strcmp(str1, str2); // -1
    printf("%d\n", ret);  // h比\0多一位
    
    ret = strcmp(str1, str3);  // 1
    printf("%d\n", ret)  // 因为g比\0少一位
}
```

## 十九. 结构化数据

数组的结构化问题用struct来解决，其次注意的是程序的交互式设计

### 19.1 结构化数据的初始

```c
#include<stdio.h>
int main()
{
	struct{
        char name[20];
        int gender;
        double height;
        double weight;
    }arr[10];  // 大概可以存储十项数据左右的交互式设计
    
    int numOfPerson = 0;
    while(1)
    {
		system("cls");
        printf("1. input person information\n");
        printf("2. display person information\n");
        printf("3. exit\n");
        int input;
        scanf("%d", &input);
        if(input == 1)
        {
			printf("input name gender height weight:\n");
             scanf("%s %d %lf %lf", arr[numOfPerson].name,&arr[numOfPerson].gender,
                  &arr[numOfPerson].height,&arr[numOfPerson].weight);
             numOfPerson++;
        }
        else if(input == 2)
        {
			printf("display personal information\n");
             printf("name gender height weight:\n");
             for (int i = 0; i < numOfPerson; i++)
             {
				printf("%s %d %.2f %.2f\n", arr[i].name, arr[i].gender, arr[i].height,
                      arr[i].weight);
             }
             system("pause");
        }
        else
        {
            break;
        }
    }
}
```

**通过构建结构体**

```c
struct{
        char name[20];  // 以下面arr为这个结构的名字，arr[10].name即可访问关于name这里的数据
        int gender;  // 同理其他的也如上面的访问方法
        double height;
        double weight;
    }arr[10]； // 代表有十个这样的数据，这十个都可以arr[10].xxxx的方法来访问更深的一层
```

### 19.2 结构

> struct：结构，一种数据类型

#### 19.2.1 结构别名

```c
struct person{
	char name[20];
    int gender;
    double height;
    double weight;
};  // 这里的person相当于一个模板
struct person timmy;  // 利用上述模板给予别名比如这里叫timmy
struct person jack;
```

**别名如果在一个函数中，只可以在内部使用，除非是指针调用地址**

#### 19.2.2 结构初始化

```c
struct person{
	char name[20];
    int gender;
    double height;
    double weight;
};
struct person timmy = {"timmy", 1, 170.00, 60};  // 依次对应结构顺序里面的顺序
```

初始化注意事项：

1. 初始化列表由花括号包括
2. 花括号内为结构成员需要被初始化的值
3. 初始化值按照结构成员声明时的顺序依次排列
4. 每个初始化之间由逗号分隔

#### 19.2.3 访问结构化数据里面的元素

```c
struct person{
	char name[20];
    int gender;
    double height;
    double weight;
};
struct person people[3] = {{"timmy", 1, 170.00, 60},
                           {"david", 1, 175.00, 65},
                           {"jane", 2, 165.00, 55},
                          };
for(int i = 0; i < 3; i++)
{
	struct person per = people[i];  // 类似Python里面对每个元素进行的访问
    printf("%s", per.name);
    printf("%d", per.gender);
    printf("%d", per.height);
    printf("%d", per.weight);
}
```

#### 19.2.4 嵌套结构

```c
struct contact
{
	char phone[20];
    char email[20];
};
struct person
{
    char name[20];
    int gender;
    double height;
    double weight;
    struct contact c;  // 这里的c是相当于结构别名
};
/* 访问时后 */
struct person per = {"timmy", 1, 170.00, 65.00,{"13823930623", "3186509188@qq.com"}}
printf("%s", per.name);
printf("%d", per.gender);
printf("%d", per.height);
printf("%d", per.weight);
printf("%s", per.c.phone);
printf("%s", per.c.email);
```

#### 19.2.5 结构的指针

```c
struct person
{
    char name[20];
    int gender;
    double height;
    double weight;
    struct contact c;  // 这里的c是相当于结构别名
};
/* 访问时后 */
struct person timmy = {"timmy", 1, 170.00, 65.00,}
struct person *pTimmy = &timmy;
printf("%s", (*pTimmy).name);
printf("%d", (*pTimmy).gender);
printf("%d", (*pTimmy).height);
printf("%d", (*pTimmy).weight);
```

**成员间接运算符->**

> (*pTimmy).name = pTimmy -> name

所以有以下代码

```c
struct person
{
    char name[20];
    int gender;
    double height;
    double weight;
    struct contact c;  // 这里的c是相当于结构别名
};
/* 访问时后 */
struct person timmy = {"timmy", 1, 170.00, 65.00,}
struct person *pTimmy = &timmy;
printf("%s", *pTimmy->name);
printf("%d", *pTimmy->gender);
printf("%d", *pTimmy->height);
printf("%d", *pTimmy->weight);
```

#### 19.2.6 结构函数传递

```c
struct person
{
    char name[20];
    int gender;
    double height;
    double weight;
};
struct person change();
{
    struct person per;
    strcpy(pername,"name");
    per.gender = 1;
    per.height = 175.00;
    per.weight = 130;
    return per
}
int main()
{
	struct person timmy = {"timmy", 1, 170.00, 65.00,};
    timmy = change();
    printf("%s\n", per.name);
    printf("%d\n", per.gender);
    printf("%.2f\n", per.height);
    printf("%.2f\n", per.weight);
    return 0;
}
```

以上是传值的方法，当然在没有return的情况下是要用指针的，不然无法改变主函数里面的东西，同样是内存的栈帧问题

```c
struct person
{
    char name[20];
    int gender;
    double height;
    double weight;
};
void change(struct person *per);
{
    strcpy(per->name, "david");
    per->gender = 1;
    per->height = 175.00;
    per->weight = 130
}
int main()
{
	struct person timmy = {"timmy", 1, 170.00, 65.00,};
    change(&timmy);
    struct person *pTimmy = &timmy
    printf("%s\n", pTimmy->name);
    printf("%d\n", pTimmy->gender);
    printf("%.2f\n", pTimmy->height);
    printf("%.2f\n", pTimmy->weight);
    return 0;
}
```

上面的代码主要是传引用的指针运用方法

## 二十. 联合与枚举

### 20.1 联合

```c
union{
    char c;
    short s;
    long long ll;
}
```

> 语法与结构差不多

**以下是结构与联合在内存上的关系**

```c
struct
{
    char c;
    short s;
    long long ll;
}s;
union{
	char c;
    short s;
    long long ll;
}u;
printf("&s.c %d\n", &s.c);  // &s.c 8649904, 这里数据的数据在内存上的地址有空缺
printf("&s.s %d\n", &s.s);  // &s.s 8649906
printf("&s.ll %d\n", &s.ll);  // &s.ll 8649912
printf("&u.c %d\n", &u.c);  // &u.c 8649896, 可见联合对于数据的存储位置貌似采用了替代的方式，重叠的
printf("&u.s %d\n", &u.s);  // &u.s 8649896
printf("&u.ll %d\n", &u.ll);  // &u.ll 8649896
```

**union的使用**

```c
struct message
{
	int type;
    union{
        int n;
        float f;
        char *str;  // 合二为一，防止信息空缺
    }u;
};
void printing(struct message msg)
{
	switch(msg.type)
    {
        case 1:
            printf("%d\n", msg.u.n);
            break;
        case 2:
            print("%f\n", msg.u.f);
            break;
        case 3:
            printf("%s\n", mag.u.str);
            break;
    }
};
int main(void)
{
	struct message msg[3];
    msg[0].type = 1;
    msg[0].n = 123;
    msg[1].type = 2;
    msg[1].f = 3.1415926;
    msg[2].type = 3;
    msg[2].str = "helloworld";
    for(int i = 0; i < 3; i++)
    {
		printing(msg[i]);
    }
    return 0;
}
```

### 20.2 枚举(enum)

```c
enum
{
	one;  // 1
    two;  // 2
    three;  // 3
}
```

**可以给这里one，two， three，进行赋值，数值也会改变**，固定为0， 1， 2， 3……

```c
enum msgType{
    eninteger = 1;
    efloat = 3;
    eString = 5;
};
struct message
{
	enum msgType type;
    union{
        int n;
        float f;
        char *str;
    }；
};
void printing(struct message msg)
{
	switch(msg.type)
    {
        case eInteger:
            printf("%d\n", msg.u.n);
            break;
        case eFloat:
            print("%f\n", msg.u.f);
            break;
        case eString:
            printf("%s\n", mag.u.str);
            break;
    }
};
int main(void)
{
	struct message msg[3];
    msg[0].type = eInteger;
    msg[0].n = 123;
    msg[1].type = eFloat;
    msg[1].f = 3.1415926;
    msg[2].type = eString;
    msg[2].str = "helloworld";
    for(int i = 0; i < 3; i++)
    {
		printing(msg[i]);
    }
    return 0;
}
```

## 二十一.标识符作用

> 1. 编译去预留sizeof(int)字节的内存空间
> 2. 标识符n指代上述的内存空间
> 3. 标识符n为int类型，用于规范所指代内存空间中的数据使用

**正确来说在于栈帧的位置，用完及消失**

```c
#include <stdio.h>
int main()
{
    {
        int n;
        printf("&n = %#p\n", &n);
    };
    {
		float n;
        printf("&n = %#p\n.", &n);
    };
}
```

上述代码当中不同的代码块之间的n的地址也不同

```c
#include<stdio.h>
int main()
{
	// 代码块A
    {
        int n;
        printf("&n = %#p\n", &n);  // 004FF96C
        // 代码块B
        {
            int n;
            printf("&n = %#p\n", &n);  // 004FF960
        }
    }
}
```

内层作用域将覆盖外层作用域，如果在代码块B后再加一个printf("&n = %#p\n", &n)，但在代码块A内，则打印的是外层覆盖域的n，所以说每一个代码块实际上是内存上的栈帧问题，先进先出。

如果是包括在函数之外的，那可以说只在main函数调用时起到作用，而函数自己有调用的话属于在函数自己的作用域内。与外面的一切均不相同

## 二十二. 预处理指令

预处理器对含有井号的文件给预处理器，传给编译器进行编译，但不会改变源码

> #define 宏 替换体

1. 宏：命名规则需要遵循标识符命名规则，当作文本处理
2. 替换体：不仅局限于值，形式丰富，替换后，代码需要能够正常编译

```c
#include<stdio.h>
#define SQUARE(x) x*x
int main()
{
	int n = 2;
    SQUARE(n); // n*n
    SQUARE(n + 2);  // 2+n*n+2,这里计算优先级是乘法
    100 / SQUARE(n);  // 100/n*n，乘除同级别，左到右
    SQUARE(++n);  // 自增不确定性：++n*++n
}
```

**所以在预处理文件上进行宏的编写，多半是有问题的**

1. 宏函数的参数应当作为一个整体，优先运算
2. 宏函数展开后的表达式应当作为一个整数
3. 结合一二点
4. 如果宏函数的替换体内多次使用参数，请不要用自增或者自减表达式

在宏函数内#与“又有不同之处

```c
#include<stdio.h>
#define FMT(varname) "the value of" varname "is %d\n""The value of" number "is %d\n";
#define FMT2(varname) "the value of" #varname "is %d\n""The value of" number "is %d\n";  // number成为了一个字符串，这个才是对的
int main()
{
	int number = 123;
    printf("the value of""number""is %d\n", number);
    printf(FMT2(number), number);  // 这个是和前面一样的, 如果是双引号则会有问题
    return 0;
}
```

**双井号，将替换体中的两个记号组合成一个记号使用**

```c
#define VARNAME(group, name) group ## name
VARNAME(group1, Apple);  // group1Apple
VARNAME(group1, Orange);  // 下面类似
VARNAME(group2, Apple);
VARNAME(group2, Orange);
```

**定义了宏之后可以在他下面#undef 宏名 取消定义**

## 二十三. typedef 关键词

> 用于定义类型别名

1. 定义于代码块内，具有代码块作用域
2. 若定义于代码块之外具有文件作用域

```c
/* 块作用域 */
#include<stdio.h>
int32_t add(int32_t a, int32_t b)
{
	return a + b;
}
int main()
{
	typedef int int32_t;
    int32_t n = 123;
    printf("n = %d\n", n);
    return 0;
}
```

```c
/* 文件作用域 */
#include <stdio.h>
typedef int int32_t;
int32_t add(int32_t a, int32_t b)
{
	return a + b;
}
int main()
{
    int32_t n = 123;
    printf("n = %d\n", n);
    return 0;
}
```

**typedef 经常用于结构**

```c
typedef struct{
    char name[20];
    int gender;
    double height;
    double weight;
}person;  // 直接声明了一个结构变量，使得往后使用不用再输入一个struct关键词，增加一个方便使用的别名
```

**#define和typedef区别**

1. #define 可以为变量设定一个别名
2. #define由预处理器处理，并且修改替代编码，typedef不受预处理影响，编译时由编译器处理
3. #define也能为类型定义别名，但某些情况下typedef情况更好

```c
#define STRING char*
STRING a1, a2;  // 这里只有第一个是指针类型
```

```c
typedef char*STRING;
STRING name1; name2;  // 这里两个都是char*类型
```

**提高可移植性**

> 整型类型的别名无需自己定义：编译器会根据本平台的整型范围大小，设置对应的别名

vs当中用头文件<inttype.h>保证可移植性

