<a name="KorT1"></a>
# C语言的基本认识
- C语言是啥？

1972年，贝尔实验室的丹尼斯·里奇（Dennis Ritch）和肯·汤普逊（Ken Thompson）在开发UNIX操作系统时设计了C语言。
把计算机和你比作不同国家的人，你想要计算机去做事帮你是做某些事，需要告诉它基于你实现的目的他该怎么去做，于是我们可以用c语言写下一条条语句（指令），告诉计算机该怎么去做。你们都不会对方的语言不能理解对方的思想，好在有一种语言你们都可以听得懂看的懂，C语言与其他得编程语言就相当于你和计算机都能懂得一种语言，你们可以用它去沟通。

- C语言与其他编程语言的区别？C语言最大特点具有汇编语言才具有得微调控能力，可直接用指针对内存操作。

**我们学习c语言,关键就是学习它的函数库该如何使用.**
C 语言能够让用户更轻松完成自顶向下，结构化编程 和 模块化设计
C 拥有具有汇编能力才具有的微调控能力
main函数总是第一个被调用的函数
函数是C语言的构造块
<a name="F4Jox"></a>
## C语言六大特性
<a name="hFQZ4"></a>
### 1.设计特性
C语言的设计理念让用户能轻松地完成自顶向下的规划、结构化编程和模块化设计
<a name="kY4Nh"></a>
### 2.高效性

- 强大的控制结构
- 快速
- 代码紧凑 ——-代表程序更小
- 可以移植到其他计算机

在设计上，它充分利用了当前计算机的优势，因此 C程序相对更紧凑，而且运行速度很快。实际上，C 语言具有通常是汇编语言才具有的微调控制能力
<a name="Rcj8P"></a>
### 3.可移植性
各种平台都可以找到合适的C语言编译器，可以直接运行或者简单修改后就可以运行。
<a name="oF9ke"></a>
### 4.强大而灵活
UNIX操作系统大部分都是由C语言写的
C程序还可以用于解决物理学和工程学问题，甚至可以用于制作电影的动画特效。
<a name="Gmk7h"></a>
### 5.面向程序员
程序员利用C语言可以访问硬件，操作内存中的位。
C语言还具有非常丰富的位运算符和众多C函数供程序员使用。
<a name="UXAhD"></a>
### 6.设计程序步骤

- 定义程序目标
- 设计程序
- 编写代码
- 编译
- 运行程序
- 测试和调试程序
- 维护和修改代码
<a name="giI1e"></a>
## C文件的运行步骤
一个写好的后缀为 .C 的文件，经过编译器编译后变成一个后缀为 .obj 的文件
然后衔接器将调用_库代码_和_启动代码_加上你编写的目标代码,合成一个后缀为.exe的文件,让计算机去执行.

- 源代码
—> 就是我们再编辑器上写好的代码.
——> 编辑器 编译器 IDE都不知道得话,自行百度.
- 库代码
—> 比如你程序中用了 strlen()函数, 那么你就得有包含这个函数的头文件 include<string.h>
——>那么程序运行时就只会再 string函数库 中提取你用到得strlen()函数代码.
- 启动代码
—> 就是我们后买你编写c语言每次都必先写得
- main (void)
- {
- }

![image.png](https://cdn.nlark.com/yuque/0/2023/png/33584294/1697625084694-0e87587c-177a-49de-846a-56bb2e107de4.png#averageHue=%23efefef&clientId=u72f33eee-b7a2-4&from=paste&id=u8bfed6a8&originHeight=627&originWidth=745&originalType=url&ratio=1.5&rotation=0&showTitle=false&size=77465&status=done&style=none&taskId=u9e2b1219-6828-4654-a267-04265fd5098&title=)
<a name="gd8Xj"></a>
## C语言书写格式
<a name="AQi04"></a>
### C语言中的两种注释
```
//  只能单行注释

/*
    可多行注释
*/
```
首先我们每次写C语言时请把下面这段代码写好
```
#include <stdio.h>    // 这个函数库提供基本的输入和输出
int main(void)                    //函数头
{
    //以下全是函数体
    //以后语句就写在这个{}括号类
    //语句一般都需要用 ; 结尾
     return 0 ;
}
```
main函数总是C语言程序执行时得第一个执行的函数.
main(void) 中的 void 也可以不写,但是我推荐还是写着.
return 0 是这个int类型的函数返回值是 0
{} 这个括号也叫 域 , return在C语言中是一种跳转语句
看不懂没关系,砸门后面还会多次了解,只用知道每次写C语言时要向上面格式折磨写.
接下来我们知道#include <stdio.h>函数每次是必写得,那么我们就可以使用这个函数库中用于输入,输出的函数
如 printf(); scanf(); getchar(); putchar();
我们先简单了解这两个函数:
printf(), 这个可以告诉计算机把你想输出的东西,打印在你电脑屏幕上.
scanf(), 这个可以接收不同的类型你输入的数据.
```
#include<stdio.h>
int main(void)
{
    char name[10];
    printf("please enter your name:\n");
    scanf("%s",&name);
    printf("Hello %s ,This is your program",name);
    return 0;
}
```
上面程序中我们有几点可能你会不熟悉
1.char name[10]; — 创建一个char类型数组名为name
这个可以看下面的变量的介绍.
2.scanf(“%s”,&name)中的 %s
% 表示占一个位置,s代表用字符形式输出.
类似的还有如下:
```
%d占一个位置,十进制输出
%f占一个位置 , 然后小数形式输出
%.2f  中的 .2 用于精确控制输出
```
<a name="GlM65"></a>
##### 声明一个变量方式
变量声明方式如下:
```
int num；          // 这代码叫做声明
int num2,num3;       // 也可以像这样一次性声明几个
/*
    int 是C语言中的数据类型
    num 叫做标识符,也就是变量名
*/
```
声明完成两件事情
**声明就是特定的标识符和计算机内存中的特定位置联系起来，同时也确定了储存在某位置的信息类型或数据类型。**

1. C语言中的所有变量必须先声明才能够使用
2. 在函数中有一个名为num的变量
3. int 表明 num 变量是一个整数
<a name="AioFc"></a>
##### C语言的有效声明
C语言中的关键字和保留标识符不能被用来给变量命名
**用小写字母、大写字母、数字和下划线 “_” 来命名。**
**而且，名称的第1个字符必须是字符或下划线，不能是数字。**
在C语言中，实际参数（简称实参）是传递给函数的特定值，形式参数（简称形参）是函数中用于储存值的变量

- C语言得名称时区分大小写的
- name // 纯英文
- name2 // 英文后面接数字
- name_three // 英文下划线接英文

**总结**
1.知道了C语言六大特性
2.C语言程序的执行过程
3.知道C语言最基本写法格式
4.知道了变量的声明方法
5.C语言中的两种注释
我们下一个系列目标:
1.将稍微仔细介绍一下C语言中各种不同类型的数据类型.
2.更加详细的介绍printf()函数 和 scanf()函数
3.学习 putchar() 和 getchar();

---

本人所写的一点破烂知识均来自(C primer plus 6) 这本书和 菜鸟教程 上的一点点.
之所以学C语言也是因为有些个人原因需要用到这门编程语言一段时间, emm…
因为我是不久决定学习编程的小白,想着把每次学的写点东西写出来.
但想到我写的东西万一能帮到别人,就每一次当作写文章在写,尽量清楚,同时锻炼自己写文章能力.
如果觉得有啥问题或者缺陷的地方欢迎评论区 补充 或者 询问.
狂神明明是教java的呀 =_= 他看见会不会说我不务正业(逃~

---

先普及点计算机一点点基本知识:
<a name="nzG0F"></a>
### 位(bit) 字节(byte) 和 字(word)
位(bit) 计算机最小储存单位,可以储存 0 或 1, 是计算机内存的基本构建块.
字节(byte) 一字节为8位 如 : 00000001
字(word) : 是设计计算机时给定的自然储存单位,个人计算机从 最开始8位—16位—32位—到现在的64位,计算机的子长越大,其数据转移越快,允许内存访问也更多.

---

之前我们明白了变量怎么创建
C语言中的变量如下:
以下变量都各自有各自的大小范围,但是那些数据我是记不清的了
也懒得去仔仔细细复制过来,就复制过来两个,想了解百度一下就好 (emm..微微一笑

- **整数类型** :
int (long short unsigned 这三个是int的变式)
unsigned 加它就是表示没有负数,取值范围就是非负数.
还有一个就是 longlong(C99时加入的) (这个我好像还没咋用过=_=
然后 int 有个很有意思的地方
**就是int要么会和short字节数一样大或者和long字节数一样大** (-反复横跳?
所以一般int要么是2字节 要么是4字节
所以取值范围: -32,768 — 32,767 or -2,147,483,648 — 2,147,483,647
根据书上说的就是会因为
- **浮点类型(小数)** :
float double ;long double
浮点类型 和 整数类型也就是存储方式不同float 存储最大字节数 : 4
float 最小值: 1.175494E-38
float 最大值: 3.402823E+38
精度值: 6
- **存字符** : char
**这个有意思,这个char存字符存的还是存的数字,本质上来说char也算个整数类型.**
char a = ‘A’; // 然后就是一般输入字符打 ‘’ 表示字符.
- **布尔类型** :
存储空间就只有一位(byte) 只存储 0 1 够了
和java一样,java里flase是flase true就是true 1就是数字1
但是在C语言中,1(非零的)就是真(ture),0就是假(false)
_Bool (引入 #include<stdbool.h> 头文件后可以直接写成 bool,也可以用true 和 false 表示1 和 0)
没引入头文件就只能用 1 或 0 表示 false true
- **枚举类型**
枚举是 C 语言中的一种基本数据类型
枚举一般被定义为 int 或者 unsigned int 类型 , 所以不能定义字符 浮点等类型.
枚举里面用逗号隔开,大括号后面要打分号结尾.
```
//定义第一个变量后,后面的变量被赋予的值都是在前一个变量的基础上 +1
     // 如果不定义第一个变量的值,就会默认值为 0 
     enum CHARATER
     {
         A = 1,B,C,D,E,F,G
     };

    // 定义枚举的同时定义枚举变量
     enum CHARATER
     { 
         A = 1,B,C,D,E,F,G 
     }letter;
    // 也可省略枚举名
     enum
     { 
         A = 1,B,C,D,E,F,G
     }letter;
```
_ Complex、_Imaginary
这两个表示复数 和 虚数 ——-(目前我都还没用到过 哭脸)
<a name="MB27E"></a>
##### 截断
```
#include　<stdio.h>
int　main(void)
{
    unsigned int un = 3000000000; /* int为32位和short为16位的系统 */
    short　end　=　200;
    long　big　=　65537;
    long　long　verybig　=　12345678908642;
    printf("un　=　%u　and　not　%d\n",　un,　un);
    printf("end　=　%hd　and　%d\n",　end,　end);
    printf("big　=　%ld　and　not　%hd\n",　big,　big);
    printf("verybig=　%lld　and　not　%ld\n",　verybig,　verybig);
    return　0;
}
/*
    在特定的系统中输出如下（不同系统输出的结果可能不同）：
    un = 3000000000 and not -1294967296
    end = 200 and 200
    big = 65537 and not 1
    verybig= 12345678908642 and not 1942899938
    该例仅仅表明，使用错误的转换说明会得到意想不到的结果。
    使用h修饰符可以显示较大整数被截断成 short 类型值的情况。第 3 行输出就演示了这种情况。把 65537 以二进制格式写成一个 32 位数是00000000000000010000000000000001。使用%hd，printf()只会查看后 16 位，所以显示的值是 1。
*/
```
类型的级别从高至低依次是
long double、double、float、unsignedlong long、long long、unsigned long、long、unsigned int、int。
例外的情况是，当 long 和 int 的大小相同时，unsigned int比long的级别高。
之所以short和char类型没有列出，是因为它们目前和 int或unsigned int相同。
小类型变大类型自动就变了
但是大转小我们就需要**强制转换**了
```
int x , y ,z;
    x = y = 10;
    printf("%d",x);    // 输出结果为 10

    x = (int)3.8 + 3.3;  //输出6
    x = (2 + 3) * 10.5;  //输出52
    x = 3/5 * 22.0;     // 0
    y = 22.0 * 3/5;     // 13
```
<a name="aJfI1"></a>
##### 整数溢出
**有符号类型整数溢出 是从最小复数从新开始.
无符号整数溢出,则是从 0 从新开始.**
所以我们一定要用适合的数据类型去存储适合的变量
```
#include　<stdio.h>
    int　main(void)
    {
    int　i　=　2147483647;
    unsigned　int　j　=　4294967295;
    printf("%d　%d　%d\n",　i,　i+1,　i+2);
    printf("%u　%u　%u\n",　j,　j+1,　j+2);
    return　0;
    }
    /*
        在我们的系统下输出的结果是：
        2147483647　　　-2147483648　 -2147483647
        4294967295　　　0　　 1
    */
```
那么有变量,那不就有常量吗? (有我灰太狼在的地方,就一定有喜羊羊 = =
<a name="hHITo"></a>
### 我们来看一看C语言常量
那这里我们就不得不提预处理 和 const关键字
最好用#define 定义数值常量，用 const 关键字声明的**变量**为只读变量。在程序中使用符号常量（明示常量），提高了程序的可读性和可维护性。
看如代码:
```
#include <stdio.h>
    #define PI 3.14159       // 使用预处理定义一个常量
    int main(void)
    {
         float area,circum,radius;
         printf("What is the radius os your pizza?\n");
         scanf("%f",&radius);
         area = PI * radius*radius;    // 面积
         circum = 2.0*PI*radius;       // 周长
         printf("your basic pizza parameters（参数） are as follow: \n");
         printf("circumference = %1.2f,area = %1.2f\n",circum,area);
         return 0;

        /*
        const int MONTHS = 12; // MONTHS在程序中不可更改，值为12
        这使得MONTHS成为一个只读值。也就是说，可以在计算中使用MONTHS，可以打印MONTHS，但是不能更改MONTHS值。const用起来比#define更灵活
        */
    }
```
书中还提到一个叫**明示常量**的东西
分别是两个头文件: #include <limit.h> #include <float.h>
**分别提供了与整数类型和浮点类型大小限制相关的详细信息。每个头文件都定义了一系列供实现使用的明示常量**
<a name="t0tGO"></a>
##### 转义字符
%% 这个就是打印一个百分号
比如:
```
\ 表示转义
\n(换行) \b(退格) \f(换页) \r(回车) \t(制表符) \v(垂直制表符) \a(警告)
\\ ,  \?  ,   \'  ,   \" 分别都是打印出这些特殊的符号 
\0(表示八进制)  \x(表示16进制)
```

---

<a name="HcjBR"></a>
## scanf() 和 printf()函数详解
**像 %d %c等 这些符号被称为 转换说明**
转换说明
输出
%a
浮点数、十六进制数和p记数法(c99/C11)
%A
浮点数、十六进制数和p记数法(C99/C11)
%c
单个字符
%d
有符号十进制整数
%e
浮点数，e记数法
%E
浮点数，e记数法
%f
浮点数，十进制记数法
%g
根据值的不同，自动选择%f或%e。%e格式用于指数小于-4或者大于或等于精度时
%G
根据值的不同，自动选择%f或%E。%E格式用于指数小于-4或者大于或等于精度时
%i
有符号十进制整数（与%d相同)
%o
无符号八进制整数
%p
指针
%s
字符串
%u
无符号十进制整数
%x
无符号十六进制整数，使用十六进制数0f
%X
无符号十六进制整数，使用十六进制数OF
%%
打印一个百分号
<a name="L5j7b"></a>
##### 修饰符
```
这个修饰符可以放在转义字符前
1.数字  %5d 就是5个字段长度(5)用来打印整数(d),若不够,它会自己扩充.
2.标记 %-10d 在字段长度为10的左边打印整数型(不加 - 号就是默认右边)
3.精度 %5.2f 字符宽度为5 小数点输出精度为 2 位数
4.h  和整数类型转换一起使用 表示short int 和 unsigned short int 类型 示例:%hu  %hx %6.4hd.
5.hh 和整数类型转换一起使用 表示short char  和 unsigned char 类型
6.l  和整数类型转换一起使用 表示long int 和 unsigned long int 类型
7.ll 和整数类型转换一起使用 表示 longlong int 和 unsigned longlong int 类型
8.L  和浮点型一起使用表示 long double  %Ld  %10.4Le
9.j  和整型转换一起使用 表示intmax_t 或 uintmax_t类型的值定义在stdint.h中  %8jx
10.t 和整型转换一起使用 表示ptrdiff_t ptrdiff_t表示两个指针差值
11.z 和整型转换一起使用 表示size_t 类型的值,size_t是sizeof函数的返回值
```
我们看看下面代码:
```
#include <stdio.h>
#define PAGES -100
// blure-模糊的  Authentic(真实的) imitation(模仿) - 真实的模仿
#define BLURE "Authentic imitation!"  
int main(void)
{
     printf("*%+d*\n", PAGES);    // %+d 中的 + 表示显示数字正负符号           
     printf("*%2d*\n", PAGES);     //只用两个字段宽打印,但是打印的常量有三个,自动扩大符合打印长度.
     printf("*%10d*\n", PAGES);    //有10个,但是这是默认把数字位于右边
     printf("*%-10d*\n", PAGES);   // 这个 - 号表示数值位于左边

     printf("=========================================\n");

     const double RENT = 3852.99;
     printf("*%f*\n", RENT);
     printf("*%e*\n", RENT);    //浮点数 e计数法
     printf("*%4.2f*\n", RENT);
     // 结果进行了四舍五入, . 左边如若实际小于,它会自动扩充.
     printf("*%3.1f*\n", RENT);
     printf("*%10.3f*\n", RENT);
     //结果进行了四舍五入,小数点左边对10代表10个位置用来答应,长度没有10个就会空着.
     printf("*%10.3E*\n", RENT);
     printf("*%+4.2f*\n", RENT);
     //%010.2f  这个10 前面的0表示以0填充多出来的
     printf("*%010.2f*\n", RENT);

     printf("=========================================\n");
     // 只给两个打印,但是打印的东西大于两个就会扩充
     printf("[%2s]\n",BLURE);
     // 给24个空位给你打印
     printf("[%24s]\n",BLURE);
     // give you 24 blank and limit five lenght to printf 
     printf("[%24.5s]\n",BLURE);
     // give you 24 blank and limit five lenght to printf ,"-" left printf. 
     printf("[%-24.5s]\n",BLURE);
     return 0;
}
```
上面都是对于printf()函数相关的一些说明
接下来我们再看看 scanf()函数
**scanf()函数所用的转换说明与printf()函数几乎相同。主要的区别是，对于float类型和double类型，printf()都使用%f、%e、%E、%g和%G转换说明。而scanf()只把它们用于float类型，对于double类型时要使用l修饰符**
```
#include <stdio.h>
int main(void)
{
    // "%d,%d" 中间看见那个逗号没? 那么你输入字符时也需要打中间得逗号
    scanf("%d,%d",num1,num2);
}
```
**最后来看个有趣的代码**:
```
#include <stdio.h>
#define FORMAT "%s! C is cool!\n"
int main()
{
    printf(FORMAT,FORMAT);

    /*输出结果如下：
    %s! C is cool!
    ! C is cool!
     说前一个变量中的%s对于后一个变量时生效的，直接打印出来了*/
}
```
<a name="QC2XF"></a>
### 修饰符
这个修饰符好理解,看下面代码中的printf() 和 scanf()以下就能明白
一个表示等待自己设置(可以设置成变量,也可以是数字),一个表示跳过.
```
#include<stdio.h>
int main(void)
{
     // printf 中的 * 号 是待自己设置.
     unsigned width,precision;
     int number = 256;
     double weight = 242.5;
     printf("Enter a field width :\n");
     scanf("%d",&width);
     printf("the number is:%*d\n ",width,number);
     printf("Now enter a width and a percision:\n");
     scanf("%d %d",&width,&precision);
     printf("weidth = %*.*f\n",width,precision,weight);

     int n1,n2,n3;
     printf("Please enter three integers:\n");
     // * 跳过输入的类容
     scanf("%*d %*d %d %d %d",&n1,&n2,&n3);
     printf("The last integer was %d %d %d\n", n1,n2,n3);

     return 0;
}


/*、
    Enter a field width :
    3
    the number is: 256
     Now enter a width and a percision:
    8 3
    weidth =  242.500
    Please enter three integers:
    2011 2012 2013 2014 2015
    The last integer was 2013 2014 2015 // 因为2011 2012 被跳过了

*/
```

---

好了 我们也像我们上次说的带你更加了解了pritf() 和 scanf()这两个函数.
那我我们接下来就是看 getchar() 和 putchar() 了
在C语言中，用getchar()读取文件检测到文件结尾时将返回一个特殊的值
即EOF（end of file的缩写）。
scanf()函数检测到文件结尾时也返回EOF。
—- getchar（）
**通常getchar（）函数返回值在0-127之间，这些值对应标准的字符集。**
如果系统能够实别扩展字符集的话，getchar（）返回值范围可以时0-255之间。
所以我们getchar（）标记文章结尾返回值定义为 -1( #define EOF (-1) )，因为不属于以上区间。
getchar()函数实际返回值的类型是int，所以它可以读取EOF字符。
EOF是一个值，标志着检测到文件结尾，并不是在文件中找得到的符号。
—- putchar（）
为我们的putchar()就是将getchar()缓冲区里的字符拿出来,打印再屏幕上
他们都只能获取和打印一个字符,往往是和循环配合使用.
don’t BB , look at the cade
```
#include<stdio.h>
int main(void)
{
    char letter;
    printf("输入26字母中的一个字母不区分大小写:");
    letter = getchar();
    printf("你输入的字符是:");
    putchar(letter);
    return 0;
}
```
<a name="hdwe0"></a>
#### 如何使用EFO判断文件是否结尾
我们看如下代码:
我们自定义一个 ‘#’ 来结束输入
```
#include<stdio.h>
int main(void)
{
     char ch;
     while (( ch = getchar() ) != '#')
         putchar(ch);
     return 0;
}
```
如果你和我一样是windows系统,按下ctrl+z就可以结束输入.
```
#include<stdio.h>
int main(void)
{
     int ch;
     while (( ch = getchar() ) != EOF)
         putchar(ch);
     return 0;
}
```

---

<a name="jCXIl"></a>
### 数组
<a name="uYu5E"></a>
## 一维数组 :
```
数据类型 数组名 [数组长度]  //其中数组长度要大于0
    double balance [5];   // 现在balance是一个可用数组 , 长度为 5
    // 声明数组元素
    double apple[3] = {1,2.5,3};
    // 不填确定长度的话数组长度就会默认是元素个数.
    double banana[] = {1,2.2,3.3};
```
<a name="sVLBI"></a>
## 二维数组
```
int array [3] [5] ; // 有三个int类型数组,这三个数组长度都是5

// 初始化数组
int a[3][4]={
     {0, 1, 2, 3} ,   /*  初始化索引号为 0 的行 */
     {4, 5, 6, 7} ,   /*  初始化索引号为 1 的行 */
     {8, 9, 10, 11}   /*  初始化索引号为 2 的行 */
};

// 这样写也可以,但是不如上面那样美观,不推荐.
int a[3][4] = {0,1,2,3,4,5,6,7,8,9,10,11};
```
<a name="PClgP"></a>
## enum(枚举)
枚举是 C 语言中的一种基本数据类型
枚举一般被定义为 int 或者 unsigned int 类型 , 所以不能定义字符 浮点等类型.
枚举里面用逗号隔开,大括号后面要打分号结尾.
```
//定义第一个变量后,后面的变量被赋予的值都是在前一个变量的基础上 +1
 // 如果不定义第一个变量的值,就会默认值为 0 
 enum CHARATER
 { 
     A = 1,B,C,D,E,F,G 
 };

// 定义枚举的同时定义枚举变量
 enum CHARATER
 { 
     A = 1,B,C,D,E,F,G 
 }letter;
// 也可省略枚举名
 enum
 { 
     A = 1,B,C,D,E,F,G 
 }letter;
```
见如下代码,可知可以直接对枚举成员调用:
```
#include <stdio.h>
    //定义第一个变量后,后面的变量被赋予的值都是在前一个变量的基础上 +1
    // 如果不定义第一个变量的值,就会默认值为 0 
    enum CHARATER
    { 
        A1 = 1,B1,C1,D1,E1,F1,G1 
    };
    // 定义枚举的同时定义枚举变量
    enum CHARATER2
    { 
        A2 = 11,B2,C2,D2,E2,F2,G2 
    }letter_2;
    // 也可省略枚举名
    enum
    { 
        A3 = 21,B3,C3,D3,E3,F3,G3
    }letter_3;

int main()
{
    // 创建一个枚举,在main方法里面声明他的变量,
    // 可以创建一个CHARATER的变量用来接收枚举元素的值.
    enum CHARATER letter;
    letter = C1;

//  不声明 一样可以直接输出
//    enum CHARATER2 letter_2;
    letter_2 = D2;

    // 枚举名不定义 一样可以直接用
    letter_3 = D3;

    printf("******************************************************\n");
    printf("letter is %d %d\n",D1,C1); 
    printf("******************************************************\n");
    printf("letter_2 is %d \n",letter_2); 
    printf("******************************************************\n");
    printf("letter_3 is %d \n",letter_3); 
    return 0;
}
```
<a name="b1xWP"></a>
### 遍历枚举
正因为连续 我们用For循环可以遍历它
```
// 遍历 CHARATER 这个枚举 
for (letter = A1; letter < G1; letter++)
        printf("%d",letter);
```
但是像如下这种没规律的枚举则不可遍历:
```
enum No_regular
{
    n_regular_one,            // 默认为 0
    n_regular_three = 33,
    n_regular_eleven         // 值是34 默认前位加1
};
```
<a name="GhHnL"></a>
### 对枚举赋值
既然我们说过枚举是一种变量类型,那么当然我们给枚举赋值时需要转换类型
```
#include <stdio.h>
    enum No_regular
    {
        n_regular_one,
        n_regular_three,
        n_regular_eleven
    };
int main()
{
    printf("没赋值之前:%d\n",n_regular_eleven);
    int a = 10;
/*
    下面这样直接赋值是不对的!!!
    n_regular_eleven = a;
*/    


// 显得声明这个枚举和他的变量
    enum No_regular n_regular_eleven;
    n_regular_eleven = (enum No_regular) a;

    printf("赋值之后:%d\n",n_regular_eleven);
    return 0;
}
```

---

<a name="nkRId"></a>
## 总结
1.我学习了关于数据类型相关知识
2.相对于上一篇文章来说深入一些的说明了一下printf()函数 he scanf()函数
3.学习了getchar() 和 putchar()两个函数基本概念和简单使用.
4.学习了数组的创建 附带 枚举的介绍
给我的下阶段任务:
写出C语言中 运算符号 符号优先级 和 逗号 运算符
简单写明关于几个循环 判断语句的使用
C语言中函数的创建和使用
