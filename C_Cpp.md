
[Memory Models for C/C++ Programmers](https://arxiv.org/pdf/1803.04432.pdf)

[Linux Perf 性能分析工具及火焰图浅析](https://zhuanlan.zhihu.com/p/54276509)

[Profiling Software Using perf and Flame Graphs](https://www.percona.com/blog/2019/11/20/profiling-software-using-perf-and-flame-graphs/)

掌握如下三个方面就应对95%的C/C++实际编程问题
* 高效的文件读写
  * 机械硬盘
  * 固态硬盘
* 高效的网络操作
  * 服务端
  * 客户端
* 高效的并发处理
  * 锁的使用
  * 并发数据结构
  * 并发编程模式

[李浩: 再谈 volatile 关键字](https://blog.csdn.net/21cnbao/article/details/114362308?spm=1001.2014.3001.5501)



C -std
* ANSI C Standard (referred to as ANSI C and C89)
* C90 (official name: ISO/IEC 9899:1990; it is the ANSI C Standard adopted by ISO; the C89 and C90 are the same things)
* C99 (ISO/IEC 9899:1999)
* C11 (ISO/IEC 9899:2011)
* C17 (ISO/IEC 9899:2018)
* The upcoming standard informally named C2x


# GCC

GCC（英文全拼：GNU Compiler Collection）

```
gcc [options] file...
```

选项：
* -pass-exit-codes ：从一个阶段以最高错误代码退出。
* --target-help ：显示特定于目标的命令行选项。
* --help={common|optimizers|params|target|warnings|[^]{joined|separate|undocumented}}[,...] ：显示特定类型的命令行选项（使用 -v --help 显示子进程的命令行选项）。
* -dumpspecs ：显示所有内置规范字符串。
* -dumpversion ：显示编译器的版本。
* -dumpmachine ：显示编译器的目标处理器。
* -print-search-dirs ：显示编译器搜索路径中的目录。
* -print-libgcc-file-name ：显示编译器配套库的名称。
* -print-file-name=<lib> ：显示库 <lib> 的完整路径。
* -print-prog-name=<prog> ：显示编译器组件 <prog> 的完整路径。
* -print-multiarch ：显示目标的规范化 GNU 三元组，用作库路径中的一个组件。
* -print-multi-directory ：显示 libgcc 版本的根目录。
* -print-multi-lib ：显示命令行选项和多个库搜索目录之间的映射。
* -print-multi-os-directory ：显示操作系统库的相对路径。
* -print-sysroot ：显示目标库目录。
* -print-sysroot-headers-suffix ：显示用于查找标题的 sysroot 后缀。
* -Wa,<options> ：将逗号分隔的 <options> 传递给汇编器（assembler）。
* -Wp,<options> ：将逗号分隔的 <options> 传递给预处理器（preprocessor）。
-Wl,<options> ：将逗号分隔的 <options> 传递给链接器（linker）。
-Xassembler <arg> ：将 <arg> 传递给汇编器（assembler）。
-Xpreprocessor <arg> ：将 <arg> 传递给预处理器（preprocessor）。
-Xlinker <arg> ：将 <arg> 传递给链接器（linker）。
-save-temps ：不用删除中间文件。
-save-temps=<arg> ：不用删除指定的中间文件。
-no-canonical-prefixes ：在构建其他 gcc 组件的相对前缀时，不要规范化路径。
-pipe ：使用管道而不是中间文件。
-time ：为每个子流程的执行计时。
-specs=<file> ：使用 <file> 的内容覆盖内置规范。
-std=<standard> ：假设输入源为 <standard>。
--sysroot=<directory> ：使用 <directory> 作为头文件和库的根目录。
-B <directory> ：将 <directory> 添加到编译器的搜索路径。
-v ：显示编译器调用的程序。
-### ：与 -v 类似，但引用的选项和命令不执行。
-E ：仅执行预处理（不要编译、汇编或链接）。
-S ：只编译（不汇编或链接）。
-c ：编译和汇编，但不链接。
-o <file> ：指定输出文件。
-pie ：创建一个动态链接、位置无关的可执行文件。
-I ：指定头文件的包含路径。
-L ：指定链接库的包含路径。
-shared ：创建共享库/动态库。
-static ：使用静态链接。
--help ：显示帮助信息。
--version ：显示编译器版本信息。



```
c99 -Wall -o getting-started getting-started.c -lm
```




 


```
#include <stdio.h>
int main() {
   printf("Hello, World!");
   return 0;
}

$ gcc hello.c -o hello
$ strace ./hello
```

 Linux 执行系统调用的三种方法：
* 使用软件中断（Software interrupt）触发系统调用；
* 使用 SYSCALL / SYSENTER 等汇编指令触发系统调用；
* 使用虚拟动态共享对象（virtual dynamic shared object、vDSO）执行系统调用；


 Michael J. Donahoo and Kenneth L. Calvertm, TCP/IP Sockets in C: Practical Guide for Programmers, 2nd Edition, Morgan Kaufmann, 2009 [source code](http://cs.ecs.baylor.edu/~donahoo/practical/CSockets2/textcode.html)




为了避免同一个文件被 #include 多次，或者避免头文件嵌套包含（参照前置声明的笔记）。需要特别注意的是：
* #pragma once 并不是C++的原生语法，而是编译器的一种支持，所以并不是所有的编译器都能够支持。#ifndef 则为C++的标准。
* #ifndef 依赖于不重复的宏名称，保证了包含在 #endif 的内容不会被重复包含，这个内容可以是一个文件的所有内容，或者仅仅是一段代码。


类型 char、wchar_t、char8_t、char16_t 和 char32_t 是内置类型，可表示字母数字字符，非字母数字字形和非打印字符。char8_t 是 C++20 中的新增功能，需要 /std:c++20 或 /std:c++latest 编译器选项。

1.ANSI C 提供了3种字符类型，分别是char、signed char、unsigned char。

# C

declarations, definitions, and statements.

All identifiers in a program have to be declared.

keywords are predefined by the language and must not be declared or redefined.

```shell
apropos printf
man printf
man 3 printf
```




```c
int main(int argc, char *argv[])
```
argc表示参数个数（argument count），而argc表示参数向量（argument vector）.

第一个参数argc是传递的参数数量加1，包括了执行程序的名字。因此，args总是大于0，而argv[0]是正在持续程序的名字（包括了路径）


printf format
* %hu、%u、%lu 以十进制、无符号的形式输出 short、int、long 类型的整数
* %hd、%d、%ld 以十进制、有符号的形式输出 short、int、long 类型的整数
* %ho、%o、%lo  以八进制、不带前缀、无符号的形式输出 short、int、long 类型的整数
* %#ho、%#o、%#lo 以八进制、带前缀、无符号的形式输出 short、int、long 类型的整数
* %hx、%x、%lx, %hX、%X、%lX 以十六进制、不带前缀、无符号的形式输出 short、int、long 类型的整数。如果 x 小写，那么输出的十六进制数字也小写；如果 X 大写，那么输出的十六进制数字也大写。
* %#hx、%#x、%#lx, %#hX、%#X、%#lX 以十六进制、带前缀、无符号的形式输出 short、int、long 类型的整数。如果 x 小写，那么输出的十六进制数字和前缀都小写；如果 X 大写，那么输出的十六进制数字和前缀都大写。
* %f、%lf 以十进制的形式输出 float、double 类型的小数
* %e、%le, %E、%lE 以指数的形式输出 float、double 类型的小数。如果 e 小写，那么输出结果中的 e 也小写；如果 E 大写，那么输出结果中的 E 也大写。
* %s   字符串 
* %c   单个字符 
* %p  指针的值 
* %g、%lg, %G、%lG   以十进制和指数中较短的形式输出 float、double 类型的小数，并且小数部分的最后不会添加多余的 0。如果 g 小写，那么当以指数形式输出时 e 也小写；如果 G 大写，那么当以指数形式输出时 E 也大写。


* %3d   表示输出3位整型数, 不够3位右对齐。 
* %9.2f 表示输出场宽为9的浮点数, 其中小数位为2, 整数位为6, 小数点占一位, 不够9位右对齐。 
* %8s   表示输出8个字符的字符串, 不够8个字符右对齐。

操作符的优先级
> ++ -- postfix increment and decrement
> () function call operator
> [] array subscript
> . structure member access
> -> structure member access through a pointer
> ++ -- prefix increment and decrement
> + - unary plus and minus
> ! logical NOT
> (type_name) cast operator
> * dereference operator
> & address-of
> * / % multiplication, division, and remainder
> + - addition and subtraction
> << >> bitwise left shift and right shift
> < <= relational operators
> >= relational operators
> == != equality operators
> && logical AND
> || logical OR
> ?: ternary conditional operator
> = assignment operator
> += -= compound assignments


&和*
* definition：用于定义数据类型
  * 指针: *
  * 引用: & 
* operator：用于运算符
  * 取值(解引用): *，当变量所代表内存空间存储的是一个内存地址时，通过取值符获得这个内存地址所存储的值。
  * 取址: &，当变量代表一个变量时，通过取址符获得这个变量数据所在的内存地址。

[var arg](https://www.tutorialspoint.com/c_standard_library/c_macro_va_arg.htm)

```c
#include <stdarg.h>

va_list arg_ptr;

type va_arg(
   va_list arg_ptr,
   type 
);
void va_end(
   va_list arg_ptr 
);
void va_start(
   va_list arg_ptr,
   prev_param 
);
```

>va_list  建参数列表
>va_start(ap, num_args) 初始化列表为传入的可变长参数
>va_arg(ap, int) 依次读取参数列表中的参数。ap指参数列表，type指转换类型
>va_end(ap) 放参数列表。


But the pointer of type void* can point to any type. All pointer types are implicitly convertible to type void*. The void* type is also called a pointer to void or a generic pointer type.

When a pointer has a value of NULL, it does not point to any other object.

The p[i] expression is equivalent to *(p+i). Using a subscript operator with an index on a pointer as in p[i] means increment a pointer by i places and dereference it.


之所以struct和union需要对齐，是为了
* 内存访问效率。内存和cache以块（2^n字节）为单位进行读写，因此对齐member的访问地址，可以一次读写就能过操作member
* 数据一致性。如果一次读写，需要访问多次内存，则可能造成数据的不不一致。

每个特定平台上的编译器都有自己的默认“对齐系数”（也叫对齐模数）。gcc中默认#pragma pack(4)，可以通过预编译命令#pragma pack(n)，n = 1,2,4,8,16来改变这一系数。
内存对齐主要遵循下面三个原则:

1. 原则1：对于struct和union来说，其第一个数据成员要放在offset==0的地方,结构体变量的起始地址能够被其最宽的成员大小整除
2. 原则2：结构体成员按自身长度自然对齐（所谓自然对齐，指的是该成员的起始位置的内存地址必须是它自身长度的整数倍）.结构体每个成员相对于起始地址的偏移能够被其自身大小整除，如果不能则在前一个成员后面补充字节
3. 原则3：结构体的总大小为结构体的有效对齐值的整数倍

结构体的有效对齐值的确定：
* 当未明确指定时，以结构体中最长成员的长度为其有效对齐值
* 当用#pragma pack(n)指定时，以n和结构体中最长成员的长度中较小者为其有效对齐值
* 当用__attribute__ ((__packed__))指定长度时，强制按照此值为结构体的有效对齐值


使用sizeof运算符可以得到struct和union的确切大小（其中包含了因内存对齐所产生的内存碎片）
可以使用offsetof宏来得到一个数据成员在结构体中的位置


built-in macros
>> __LINE__
>> __FILE__
>> __TIME__ 
>> __DATE__
>> __STDC_VERSION__
>> __func__

function-like macro

visibility, scope, storage, and lifetime. 



宏调用 

inline

static inline

extern inline

visibility用于设置动态链接库中函数的可见性，将变量或函数设置为hidden，则该符号仅在本so中可见，在其他库中则不可见
```c++
__attribute__((visibility("default")))  //默认，设置为：default之后就可以让外面的类看见了。
__attribute__((visibility("hideen")))  //隐藏
```

__attribute__ ((visibility ("default")))


# Memory Model

在 C11/C++11 中，引入了六种不同的 memory order，可以让程序员在并发编程中根据自己需求尽可能降低同步的粒度，以获得更好的程序性能。这六种 order 分别是：
>> relaxed, acquire, release, consume, acq_rel, seq_cst


# Courses

 [南科大课堂原版 - C/C++：从基础语法到优化策略（2021年秋季版本）](https://www.bilibili.com/video/BV1Vf4y1P7pq?p=1)

 https://github.com/ShiqiYu/CPP



[黑马程序员-Linux系统编程](https://www.bilibili.com/video/BV1KE411q7ee?p=1)

[Linux系统编程（李慧琴）](https://www.bilibili.com/video/BV1yJ411S7r6?from=search&seid=13482678134358786324&spm_id_from=333.337.0.0)